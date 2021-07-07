#Authz Requirements

## Policies

### Gigya Authorization [b2e, b2c]
Manage Gigya Apis authorization

#### Access Control List 
- ACL inherent  
    - API
    - API Group 
    - Known roles (everyone/ developers/ admins/ social)
    - Custom groups manged by customer 
    * diagram
    
- ACL can be assigned to:
    - Admin user
    - Application key
    - Session Token 
    - Anonymous
       

- ACL API format 
    - Resource API (accounts.getAccountInfo)
    - REST API 
    - JSON 
 
 namespace, endpoint
    *example
           
- ACL can grant or ungrant access to  
    - API
        - Endpoint
        - HTTP Method
        - API's parameters
        - API's parameters values 
    
    - Claims (e.g. Skip RBA roles, search highrate users ) 
  
    - Entity Permissions (account)
        - JSON response fields
        - JSON request fields

#### Scope
- Global
- Partner
- Site
     

#### Management
-  Developer can assign ACL to a known group (except developers) --*** 
-  Admins can assign ACL to groups in a scope of a specific partner or site
-  Admins can assign only ACL that is included in their permissions
-  Admins can create and edit custom ACLs 
      
- Auto provisioning
- Auto provisioning of ACL via saml login to console 

###  Customer Provisioning Authorization [b2b, b2e, b2c]

Provide authorization claims for customer
####  Provisioning
Roles and attributes should be accessible to customer application
- VIA Oidc 
- VIA Saml
- VIA Api

#### Scope
- Partner
- Site
- Group - Organization
- Application
- Account
    
#### Role-based  
- determines access by the role of the requester. 
> e.g. managers can view organization members

- mange roles in organization context
> e.g. Meny is a manager in HR group and viewer in IT resources group

 
#### Attribute-based   
- **Subject**: attributes that describe the user attempting the access 
> e.g. age, department
- **Action**: attributes that describe the action being attempted 
> e.g. read, view
- **Object**: attributes that describe the account being accessed to 
> e.g. group, department, verified
- **Contextual**: attributes that deal with time, location or session 
>  e.g  account which is logged in a specific organization unit 
    - account is logged in via specific auth method

#### Management
- Admins can assign role to a specific user
- Admins can assign assets to a specific user
- Admins can create policy
- Admins can invite end user to edit organization's policies by assign specific role-> delegated admin
- Delegated admin can create and edit policies in their organization context

## Non Functional Requirements

- Support at least X-rps for authorization requests
- Availability in Russia and China 
- Availability SLA: 
- Should also support rate limiting 
- Multi-tenant architecture: partner, site, organization, application
- Support Import & Export policies (backup)
- Console UI integration – we need to make the CDC console and AuthZ console act like a one system.
this can be done using Ifreams or SSO flows between the systems.
- API based solution – all operations that can be done through the UI can be done using rest API's
- Dynamic schema support.
- Application management and context support – in which application what's my entitlement.
 , pii data deletion , auto provisioning , etc ?
