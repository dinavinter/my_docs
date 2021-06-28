requesting                             authorization resource resource
  party        client                      server     server    owner
    |            |                           |          |         |
    |            |                           |Set policy|         |
    |            |                           |conditions (anytime)|
    |            |                           |<- - - - - - - - - -|
    |            | Resource request (I want to see importent/data)    
    |            |------------------------------------->|         |
    |            |401 response with initial permission  |         |
    |            |ticket, authz server location         |         |
    |            |<-------------------------------------|         |
    |            |  RPT Request                  	    |         |    
	|            |  # resource: importent/data 
					# actions: see             
					# audience:rs.com          
    |            |with permission ticket                |         |        
    |            |  #  context:id  
	                #  sub:user 

    |            |claim token (push claims)             |         |
    |            |  #   rs claims             |         |         |
    |            |-------------------------->|          |         |
    |            |                      +----|Authz     |         |
    |            |                      +--->|assessment|         |
    |            |403 response with new      |          |         |
    |            |permission ticket,   
    |            |  # context: id    
    |            |  # sub: user   
    |            |  # rpt reference     
	|            |  # required step up                  |
    |            |need_info                   |         |         |
    |            |  # acr: [otp, ftp] 
	|            |  # freindly: we need step up 
    |            |redirect_user hint (go to gigya/stepup)         |          |         |
    |            |<--------------------------|          |         |
    |Redirect    |                           |          |         |
    |user with   |                           |          |         |
    |permission  |                           |          |         |
    |ticket      |                           |          |         |
    |<-----------|                           |          |         |
    |Follow redirect to authz server         |          |         |
    |--------------------------------------->|          |         |
    |Interactive claims gathering  
    | #gigya/auth/authorize?pt
	| #gigya/auth/otp
	| #gigya/auth/token/pt
    |<- - - - - - - - - - - - - - - - - - - >|          |         |
    |Redirect back with new permission ticket           |         |         |
    |	 # client/redirect 
	|    # pt + amr:otp                                 |
    |<---------------------------------------|          |         |
    |Follow      |                           |          |         |
    |redirect    |                           |          |         |
    |to client   |                           |          |         |
    |----------->|                           |          |         |
    |            |RPT request with permission|          |         |
    |            |ticket                     |          |         |
    |            |-------------------------->|          |         |
    |            |                      +----|Authz     |         |
    |            |                      +--->|assessment|         |
    |            |Response with RPT and PCT  |          |         |
    |            |<--------------------------|          |         |
    |            |Resource request with RPT  |          |         |
    |            |------------------------------------->|         |
    |            |Protected resource         |          |         |
    |            |<-------------------------------------|         |
