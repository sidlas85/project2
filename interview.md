..
CLOUD ACCESS CONTROL
Cloud Access Control - provides centralized management, visibility, and control without the cost and 
complexity of traditional physical access systems.  Plus, they provide integrations with the software
your company uses for its operations, visitor management, and door scheduling. Most security
professionals understand how critical access control is to their organization. But not everyone agrees
on how access control should be enforced.  Access control requires the enforcement of
persistent policies in a dynamic world without traditional borders. Most of people work
in hybrid environments where data moves from on-premises servers or the cloud to offices, homes, 
hotels, cars and coffee shops with open wi-fi hot spots, which can make enforcing access control difficult.

 Methods on how you control access to a cloud network :Know what you're responsible for - All 
cloud services aren't the same, and the level of responsibility varies. Software-as-a-service (SaaS)
providers make sure their applications are protected and that the data is being transmitted and
stored securely, but that's not always the case with IaaS environments. For example, an enterprise
responsibility over its AWS Elastic Compute Cloud (EC2), Amazon EBS and Amazon Virtual 
 Private Cloud (VPC) instances, including configuring the operating system, managing applications,
and protecting data. In contrast, Amazon maintains the operating system and applications for S3 
and the enterprise is responsible for managing the data, access control and identity policies. Amazon
provides the tools for encrypting the data for S3, but it's up to the organization to enable the 
protection as it enters and leaves the server.


Improve visibility - Major cloud providers all offer some level of logging tools, so make sure to turn 
on security logging and monitoring to see unauthorized access attempts and other issues. For example, 
Amazon provides CloudTrail for auditing AWS environments, but too many organizations 
don't turn on this service. When enabled, CloudTrail maintains a history of all AWS API calls, 
including the identity of the API caller, the time of the call, the caller's source IP address, the request
parameters, and the response elements returned by the AWS service. It can also be used for change 
tracking, resource management, security analysis and compliance audits.


Adopt a shift-left approach to security - The shift-left movement advocates incorporating security 
considerations early into the development process versus adding security in the final stages of 
development. "Not only should enterprises monitor what they have in IaaS platforms, they should 
be checking all their code that's going into the platform before it goes live," says McAfee's Flaherty.
"With shift-left, you're auditing for and catching potential misconfigurations before they become an 
issue." Look for security tools that integrate with Jenkins, Kubernetes and others to automate the 
auditing and correction process.

Protect the data - Another common mistake is to leave data unencrypted on the cloud. Voter
information and sensitive Pentagon files have been exposed because the data wasn't encrypted and 
the servers were accessible to unauthorized parties. Storing sensitive data in the cloud without 
putting in place appropriate controls to prevent access to a server and protecting the data is 
irresponsible and dangerous. Where possible, maintain control of the encryption keys. While it's
possible to give cloud service providers access to the keys, the responsibility of the data lies with the 
organization.Even when cloud providers offer encryption tools and management services, too many  
companies don't implement it. Encryption is a fail-safe even if a security configuration fails and the 
data falls into the hands of an unauthorized party, the data can't be used.

Secure the credentials - Create unique keys for each external service and restrict access following 
Make sure the keys don't have broad permissions. In the wrong hands, they can be used to access 
sensitive resources and data. Create IAM roles to assign specific privileges, such as making API 
calls.Make sure to regularly rotate the keys, to avoid giving attackers time to intercept compromised 
keys and infiltrate cloud environments as privileged users.Don't use the root user account, not even 
for administrative tasks. Use the root user to create a new user with assigned privileges. Lock down 
the root account (perhaps by adding multi-factor authentication [MFA]) and use it only for specific 
account and service management tasks. For everything else, provision users with the appropriate 
permissions. Check user accounts to find those that aren't being used and then disable them. If no 
one is using those accounts, there's no reason to give attackers potential paths to compromise.



