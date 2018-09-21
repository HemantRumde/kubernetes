#  AWS Users and Group
Add new AWS group for kops administration
```
aws iam create-group --groupname kops
```
# Set required privileges to newly created group 
```
aws iam attach-group-policy --group-name kops --policy-arn  arn:aws:iam::aws:policy/AmazonEC2FullAccess
aws iam attach-group-policy --group-name kops --policy-arn  arn:aws:iam::aws:policy/AmazonS3FullAccess
aws iam attach-group-policy --group-name kops --policy-arn  arn:aws:iam::aws:policy/AmazonVPCFullAccess
aws iam attach-group-policy --group-name kops --policy-arn  arn:aws:iam::aws:policy/IAMFullAccess
```
Add new user for kops administration and add it to newly created group
```
aws iam create-user --user-name kopsmgr
aws iam add-user-to-group --user-name kopsmgr --group-name kops
```
