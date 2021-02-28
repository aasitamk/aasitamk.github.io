# EXERCISE 1

--

## Description

> Infosec identified a security incident related to the leakage of AWS credentials.<br>
> The Incident Lead must carry out the steps 1 to 4 below to contain or prevent a possible attack.

## Procedure

#### STEP 1 - Remove all permissions from the affected AWS user. Credentials must not be revoked at this stage.

**1.1-** Find a user with the permission to administer IAM permissions:<br/>
```nu sec iam show group infosec-permissions-admin```
  
**1.2-** Request the removal of the inline policies from the affected IAM user:<br/>
```nu sec iam disallow <user> Source```
  
**1.3-** Request a listing of the IAM groups for the affected user:<br/>
```nu sec iam show <user>```
  
**1.4-** Request the removal of the affected IAM user from all listed groups:<br/>
```nu sec iam remove <user> <groups>```
  
#### STEP 2 - Notify the relevant stakeholders via the Slack platform.

**2.1.** Send the following message to the affected user:<br/>
*"Your AWS permissions have been temporarily suspended pending an investigation into a possible compromise. If you have any questions, please contact us. We request  confidentiality until Infosec releases the investigation results."*
  
**2.2.** Send the following message to the affected user’s manager:<br/>
*"The Nubanker {name}’s AWS account permissions have been temporarily suspended pending an investigation into a possible compromise. We request you to support the Nubanker through understanding the incident and keeping it confidential until Infosec releases the investigation results."*
  
#### STEP 3 - Revoke the affected AWS credentials.

**3.1.** Find a user with the permission to administer IAM permissions:<br/>
```nu sec iam show group infosec-permissions-admin```
  
**3.2.** Request the deletion of the affected credentials using the AWS console:<br/>
```nu sec iam delete <user> Source```
  
#### STEP 4 – Provide the affected user with new credentials.

**4.1.** Generate a new keypair (public key + private key) via AWS console.

**4.2.** Send the new keypair to the affected user via Slack direct message.

**4.3.** Instruct the affected user to update his AWS Keys in all places they are referenced to, such as the *.bash_profile*. This action can be performed using the *setupnu.sh* shell script, available in the [Nubank Github](https://github.com/nubank).

Refer to the [AWS Developer Guide](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html) for further information about working with AWS credentials.

---

# EXERCISE 2

-

## API Document Template

API documentation for the `findNeedles` method.

### Find Needles in a Haystack

The `findNeedles` method counts the number of occurrances of up to five specific words (*needles*) within a given text (*haystack*).

Here is a sample with a Java code snippet, followed by details of its parameters and the possible outputs:

**METHOD:** `findNeedles`
```java
public static void findNeedles(String haystack, String[] needles) {
   if (needles.length > 5) {
      System.err.println("Too many words!");
   } else {
      int[] countArray = new int[needles.length];
      for (int i = 0; i < needles.length; i++) {
         String[] words = haystack.split("[ \"\'\t\n\b\f\r]", 0);
         for (int j = 0; j < words.length; j++) {
            if (words[j].compareTo(needles[i]) == 0) {
            countArray[i]++;
            }
         }
      }
      for (int j = 0; j < needles.length; j++) {
      System.out.println(needles[j] + ": " + countArray[j]);
      }
   }
}
```

|PARAMETER|DESCRIPTION|TYPE|REQUIRED|
|---|---|---|---|
|`haystack`|Text to be inspected.|string|yes|
|`needles`|Words to be searched within the given text.|string|yes|

<br/>**POSSIBLE OUTPUTS:**

* For **up to 5** needles searched, the output displays the number of ocurrances for each needle:
<br/>`[needle_value]: [total_ocurrances]`

* If **more than 5** needles are searched, the output displays the following error message:
<br/>`"Too many words!"`

