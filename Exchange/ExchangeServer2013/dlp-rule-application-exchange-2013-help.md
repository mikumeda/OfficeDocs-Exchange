---
title: 'How DLP rules are applied to evaluate messages: Exchange 2013 Help'
TOCTitle: How DLP rules are applied to evaluate messages
ms.author: serdars
author: msdmaguire
manager: serdars
ms.reviewer:
ms.topic: article
description: How DLP rules are applied to evaluate messages in Exchange 2013
ms.assetid: 1ac77020-26ff-410c-ab09-4f28a99d67a1
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# How DLP rules are applied to evaluate messages in Exchange 2013

_**Applies to:** Exchange Server 2013_

You can set up sensitive information rules within your Microsoft Exchange data loss prevention (DLP) policies to detect specific data in email messages. This topic will help you understand how these rules are applied and how messages are evaluated. You can avoid workflow disruptions for your email users and achieve a high degree of accuracy with your DLP detections if you know how your rules are enforced. Let's use the Microsoft-supplied credit card information rule as an example. When you activate a transport rule or DLP policy, the Exchange transport rules agent compares messages that users send with the rule sets you create.

## Get precise about your needs

Suppose you need to act on credit card information in messages. The actions you take once those messages are found are not the subject of this topic, but you can learn more about that in [Transport rule actions in Exchange 2013](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md). You need to ensure what's detected in a message is truly credit card data and not something else (for example, a reservation code or a vehicle identification number). To meet this need, let's make it clear that the following information should be classified as a credit card:

> Margie's Travel, <br/><br/> I have received updated credit card information for Spencer. <br/> Spencer Badillo <br/> Visa: 4111 1111 1111 1111 <br/> Expires: 2/2012 <br/><br/> Please update his travel profile. **

Let's also make it clear that the following information shouldn't be classified as a credit card:

> Hi Alex, <br/><br/> I expect to be in Hawaii too. My booking code is 1234 1234 1234 1234 and I'll be there on 3/2012. <br/><br/> Regards, Lisa

The following XML snippet shows how these needs are currently defined in a sensitive information rule that's provided with Exchange:

```XML
<Entity id="50842eb7-edc8-4019-85dd-5a5c1f2bb085" patternsProximity="300" recommendedConfidence="85">
      <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_credit_card" />
        <Any minMatches="1">
          <Match idRef="Keyword_cc_verification" />
          <Match idRef="Keyword_cc_name" />
          <Match idRef="Func_expiration_date" />
        </Any>
      </Pattern>
    </Entity>
```

### Pattern-matching in your solution

The XML rule definition shown earlier includes pattern-matching, which improves the likelihood that the rule will detect only the important information and not detect vague, related information. For more information about the XML schema for DLP rules and templates, see [Define your own DLP templates and information types](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md).

In the credit card rule, there's a section of XML code for patterns, which includes a primary identifier match and other corroborative evidence. All three of these requirements are explained here:

1. `<IdMatch idRef="Func_credit_card" />`: This line requires a match of a function, titled credit card, that is internally defined. This function includes a couple of validations as follows:

   1. It matches a regular expression (in this instance for 16 digits) that could also include variations like a space delimiter so that it also matches **4111 1111 1111 1111** or a hyphen delimiter so that it also matches **4111-1111-1111-1111**.

   2. It evaluates the Lhun's checksum algorithm against the 16-digit number to ensure the likelihood of this being a credit card number is high.

   3. It requires a mandatory match, after which corroborative evidence is evaluated.

2. `<Any minMatches="1">`: This section indicates that the presence of at least one of the following items of evidence is required.

3. The corroborative evidence can be a match of one of these three statements:

   - `<Match idRef="Keyword_cc_verification"/>`
   - `<Match idRef="Keyword_cc_name"/>`
   - `<Match idRef="Func_expiration_date"/>`

    These three statements mean a list of keywords for credit cards, the names of the credit cards, or an expiration date is required. The expiration date is defined and evaluated internally as another function.

## The process of evaluating content against rules

The five steps here represent actions that Exchange takes to compare your rule with email messages. For our credit card rule example, the following steps are taken.

|Step|Action|
|---|---|
|1. Get Content|Spencer Badillo  <br/> Visa: 4111 1111 1111 1111  <br/> Expires: 2/2012|
|2. Regular Expression Analysis|4111 1111 1111 1111 -\> a 16-digit number is detected|
|3. Function Analysis| 4111 1111 1111 1111 -\> matches checksum  <br/>  1234 1234 1234 1234 -\> doesn't match|
|4. Additional Evidence|Keyword Visa is near the number. A regular expression for a date (2/2012) is near the number.|
|5. Verdict|A regular expression that matches a checksum. Additional evidence increases confidence.|

Corroborating evidence (for example, keywords) are required in the message content to match the rule. The following content is detected as not containing a credit card:

> Margie's Travel, <br/><br/> I have received updated information for Spencer. <br/> Spencer Badillo <br/> 4111 1111 1111 1111 <br/><br/> Please update his travel profile.

You can use a custom rule that defines a pattern without extra evidence. This example would detect messages with a credit card number only without any corroborating evidence.

```xml
      <Pattern confidenceLevel="85">
         <IdMatch idRef="Func_credit_card" />
      </Pattern>
    </Entity>
```

You can also extend the examples of credit cards in this article to other sensitive information rules. To see the complete list of the Microsoft-supplied rules in Exchange, use the [Get-ClassificationRuleCollection](/powershell/module/exchange/get-classificationrulecollection) cmdlet in the Exchange Management Shell. For example:

```powershell
$rule_collection = Get-ClassificationRuleCollection

[System.IO.File]::WriteAllBytes('oob_classifications.xml', $rule_collection[0].SerializedClassificationRuleCollection)
```

## For more information

[Data loss prevention](data-loss-prevention-exchange-2013-help.md)

[Transport rules in Exchange 2013](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Exchange Management Shell](/powershell/exchange/exchange-management-shell)
