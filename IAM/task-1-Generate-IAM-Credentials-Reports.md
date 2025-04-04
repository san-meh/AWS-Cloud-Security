# Generate IAM Credentials Reports

    - This project helps to generate the AWS credential report using AWS CLI.

## Configure AWS CLI

    - Download the AWS CLI access key from the IAM->user-> security credential-> generate access key for cli.

### Install AWS CLI
    
- Write command 
```bat
aws configure
```

- Genrate AWS report
```bat
aws iam generate-credential-report
```

- Get report
```bat
aws iam get-credential-report
```
- Convert the report in readable format
```bat
aws iam get-credential-report --output text --query Content | base64 -D | awk -F, '
NR==1 {next}
{
    print "User:", $1;
    print "ARN:", $2;
    print "Creation Time:", $3;
    print "Password Enabled:", $4;
    print "Password Last Used:", $5;
    print "Password Last Changed:", $6;
    print "Password Next Rotation:", $7;
    print "MFA Active:", $8;
    print "Access Key 1 Active:", $9;
    print "Access Key 1 Last Rotated:", $10;
    print "Access Key 1 Last Used Date:", $11;
    print "Access Key 1 Last Used Region:", $12;
    print "Access Key 1 Last Used Service:", $13;
    print "Access Key 2 Active:", $14;
    print "Access Key 2 Last Rotated:", $15;
    print "Access Key 2 Last Used Date:", $16;
    print "Access Key 2 Last Used Region:", $17;
    print "Access Key 2 Last Used Service:", $18;
    print "Cert 1 Active:", $19;
    print "Cert 1 Last Rotated:", $20;
    print "Cert 2 Active:", $21;
    print "Cert 2 Last Rotated:", $22;
    print "-------------------"
}' 
```

### Conclusion
It helps to monitor users credetial activity about when they and login and when they have changed the passwords
