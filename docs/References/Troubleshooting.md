---
sidebar_position: 4
---
# Troubleshooting
## OAuth Errors
### Need admin approval: Subscription Management needs permission to access resources in your organization that only an admin can grant.
Subscription Management AD application requesting `user.profile` permissions to operate. For some tenants, these permissions will require admin consent. In that case, a user with AD admin privileges should perform the signup process. 

### AADSTS53003: Access has been blocked by Conditional Access policies. The access policy does not allow token issuance. 
Subscription Management authenticates customers using [OAuth 2.0 Authorization Code with PKCE](https://tools.ietf.org/html/rfc7636) flow which includes obtaining an access token that allows an application to access user profile information. For some tenants, this capability is conditional and defined by Active Directory [Conditional Access policies](https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/concept-conditional-access-policy-common). If an AADSTS53003 error appears, it is presumably due to such a conditional policy. To resolve it, [the user who performs an activation should be excluded](https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/concept-conditional-access-users-groups#exclude-users) from such policy. [More information](https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/troubleshoot-conditional-access) on troubleshooting sign-in problems with Conditional Access.