# EXERCISE 1

--

# Compromised AWS Account Credentials

## Description

> A security incident related to the leakage of AWS credentials has been indentified by **Infosec**.<br>
> The steps 1 to 4 below must be carried out in order to contain or prevent a possible attack.

## Procedure

#### **STEP 1** - Remove all permissions from the affected AWS user without revoking credentials:

**1.1-** Find a user authorized to administer IAM permissions:<br/>
```nu sec iam show group infosec-permissions-admin```
  
**1.2-** Request the removal of the inline policies from the affected IAM user:<br/>
```nu sec iam disallow <user> Source```
  
**1.3-** Request a list of the IAM groups the affected user is part of:<br/>
```nu sec iam show <user>```
  
**1.4-** Request the removal of the affected IAM user from all listed groups:<br/>
```nu sec iam remove <user> <groups>```
  
#### **STEP 2** - Communicate the incident to the relevant stakeholders.

#### **STEP 3** - Send a Slack message to the affected user:

*"Your AWS permissions have been temporarily suspended pending an investigation into a possible compromise. Contact me if you have any questions and please keep the incident private until* the all clear *is given by Infosec."*
  
#### **STEP 4** - Send a message through the affected user’s Slack profile to their Tech/Eng Manager:

*"There has been wrongful activity using this engineer's AWS account. Please inform them that permissions associated with it have been temporarily blocked, and direct them through further understanding the incident. Please advise them to keep the incident private until* the all clear *is given by Infosec."*
  
#### **STEP 5** - Request an authorized user (STEP 1.1) to revoke the affected AWS credentials using the AWS console. 
  
#### **STEP 6** – Generate new credentials and a new keypair via AWS console.

#### **STEP 7** - Send the new keypair to the affected user via Slack direct message and instruct them to update all references to their AWS keys, like the ones in the *.bash_profile*. Such action can be performed using the *setupnu.sh* shell script, available at [Nubank Github](https://github.com/nubank).

Refer to the [AWS Developer Guide](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html) for further information about working with AWS credentials.

## Sequence Diagram

![diagram](https://aasitamk.github.io/diagram.png)

---

# EXERCISE 2

-

## API Document Template

API documentation for the `findNeedles` method.

### Finding Needles in a Haystack

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

* For **up to 5** needles searched, the output displays the number of occurrances in the haystack for each needle:
<br/>`[needle_value]: [total_ocurrances]`

* If **more than 5** needles are searched, the output displays the following error message:
<br/>`"Too many words!"`

