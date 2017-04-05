# Turn off MultiViews
Options -MultiViews

# Directive to ensure *.rdf files served as appropriate content type,
# if not present in main apache config
AddType application/rdf+xml .rdf
AddType text/turtle .ttl

# Rewrite engine setup
RewriteEngine On
RewriteBase /tsnchange

# Rewrite rule to serve HTML content from the vocabulary URI if requested
RewriteCond %{HTTP_ACCEPT} !application/rdf\+xml.*(text/html|application/xhtml\+xml)
RewriteCond %{HTTP_ACCEPT} text/html [OR]
RewriteCond %{HTTP_ACCEPT} application/xhtml\+xml [OR]
RewriteCond %{HTTP_USER_AGENT} ^Mozilla/.*
RewriteRule ^ontology/$ index.html [R=303]

# Rewrite rule to serve directed HTML content from class/prop URIs
RewriteCond %{HTTP_ACCEPT} !application/rdf\+xml.*(text/html|application/xhtml\+xml)
RewriteCond %{HTTP_ACCEPT} text/html [OR]
RewriteCond %{HTTP_ACCEPT} application/xhtml\+xml [OR]
RewriteCond %{HTTP_USER_AGENT} ^Mozilla/.*
RewriteRule ^ontology/(.+) index.html#$1 [R=303,NE]


# Rewrite rule to serve RDF/XML content from the vocabulary URI if requested
RewriteCond %{HTTP_ACCEPT} application/rdf\+xml
RewriteRule ^ontology/ ontologies/tsnchange-ontology.rdf [R=303]

# Rewrite rule to serve text/turtle content from the vocabulary URI if requested
RewriteCond %{HTTP_ACCEPT} text/turtle
RewriteRule ^ontology/ ontologies/tsnchange-ontology.ttl [R=303]

RewriteRule ^ontology/ ontologies/tsnchange-ontology.ttl
