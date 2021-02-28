# EXERCISE 1

## Incident Description:

A security incident related to the leakage of AWS credentials has been identified by Infosec. A possible attack must be either contained or prevented through the articulation of the steps contained in the procedures below.

### For the Infosec Incident Lead

#### Procedure:

##### Step 1 - Remove all permissions from the affected AWS user (do not revoke their credentials).

  **1.1.** Find an Infosec user with the *admin* role:
  ```
  nu sec iam show group infosec-permissions-admin
  ```
  
  **1.2.** Request the removal of all inline policies from the affected IAM user:
  ```nu sec iam disallow <user> Source```
  
  **1.3.** Request the identification of all IAM groups for the affected user:
  ```nu sec iam show <user>```
  
  **1.4.** Request the removal of the affected user from all groups:
  ```nu sec iam remove <user> <groups>```
  
##### Step 2 - Notify the relevant stakeholders via Slack tool.

  2.1. Send the following message to the affected user:
  *"Your AWS permissions have been temporarily suspended pending an investigation into a possible compromise. If you have any questions, please contact us. We request  confidentiality until Infosec releases the investigation results."*
  
  2.2. Send the following message to the affected user’s Tech Manager/Eng. Manager:
  *"The user <user_name>’s AWS account permissions have been temporarily suspended pending an investigation into a possible compromisse. We request you to support the employee through understanding the incident and keeping it private until Infosec releases the investigation results."*
  
**Step 3 - Revoke the affected AWS credentials.**

  3.1. Find a user with *admin* access and permissions:
  ``` nu sec iam show group infosec-permissions-admin```
  
  3.2. Request the deletion of the affected credentials using the AWS console:
  ```nu sec iam delete <user> Source```
  
**Step 4 – Provide the affected user with new credentials.**

  4.1. Generate a new keypair (public key + private key) via AWS console.

  4.2. Send the new keypair to the affected user via Slack direct message.

  4.3. Instruct the affected user into updating his AWS Keys in all places they are referenced to, such as the *.bash_profile*. This action can be performed using nudev/setupnu.sh (*https://github.com/nubank/nudev/blob/master/setupnu.sh* or *https://github.com/nubank/nu-setup*).

Refer to the [AWS SDK for Java](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html) developer guide for further information about working with credentials.

---

# EXERCISE 2

# API Document Template

API documentation for the **_`findNeedles`_** method.

## Find Needles in a Haystack

The **_`findNeedles`_** method counts the number of occurrances of up to five specific words (*needles*) within a given text (*haystack*).

Here is a sample with a Java code snippet, followed by details of its parameters and the possible outputs:

**METHOD:** *`findNeedles`*
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

* For **up to 5** needles searched, the output displays the number of ocurrances of each needle:
<br/>`[needle_value]: [total_ocurrances]`

* If **more than 5** needles are searched, the output displays an error with the following message:
<br/>`"Too many words!"`

