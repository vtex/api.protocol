## Para uma requisição sem o header Authorization:  

Bearer realm="VtexID"  

## Se o token não possuía as permissões necessárias para garantir o acesso:  

Bearer realm="VtexID",  
       error="invalid_scope",  
       error_description="The request requires other privileges than provided by the access token."  

## Se o token enviado era inválido:  

Bearer realm="VtexID",  
       error="invalid_token",  
       error_description="The access token expired."  
