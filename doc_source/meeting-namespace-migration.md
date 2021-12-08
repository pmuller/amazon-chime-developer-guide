# Migrating to the Amazon Chime SDK Meetings namespace<a name="meeting-namespace-migration"></a>

The [Amazon Chime SDK Meetings](https://docs.aws.amazon.com/chime/latest/APIReference/API_Operations_Amazon_Chime_SDK_Meetings.html) namespace is a dedicated place for the APIs that create and manage Amazon Chime SDK meetings\. You use the namespace to address Amazon Chime SDK meeting API endpoints in any Region in which they're available\. Use this namespace if you're just starting to use the Amazon Chime SDK\.

Existing applications that use the [Amazon Chime](https://docs.aws.amazon.com/chime/latest/APIReference/API_Operations_Amazon_Chime.html) namespace may continue to do so, but you should plan to migrate to the new namespace in order to use updated APIs and new features\.

**Topics**
+ [Reasons to migrate](#migration-reasons)
+ [Before you migrate](#before-migrating)
+ [Differences between the namespaces](#namespace-differences)

## Reasons to migrate<a name="migration-reasons"></a>

We encourage you to migrate to the [Amazon Chime SDK Meetings](https://docs.aws.amazon.com/chime/latest/APIReference/API_Operations_Amazon_Chime_SDK_Meetings.html) namespace for these reasons:

**Choice of API Endpoint**  
The Amazon Chime SDK Meetings namespace is the only API namespace which can use API endpoints in any [region that makes them available](https://docs.aws.amazon.com/chime/latest/dg/chime-sdk-available-regions.html)\. If you want to use API endpoints other than US\-EAST\-1, you must use the Amazon Chime SDK Meetings namespace\.  
For more information about how Amazon Chime SDK meetings use AWS regions, refer to [Meeting Regions](https://docs.aws.amazon.com/chime/latest/dg/chime-sdk-meetings-regions.html) in this guide\.

**Updated and new meeting APIs**  
We only add or update meeting APIs in the Amazon Chime SDK Meetings namespace\. We fully support the meeting APIs in the Amazon Chime namespace, but they remain as\-is\.

## Before you migrate<a name="before-migrating"></a>

Before you migrate, be aware of the differences between the namespaces\. The following table lists and describes them\.


|  | Amazon Chime SDK Meetings namespace | Amazon Chime namespace | 
| --- | --- | --- | 
| AWS SDK namespace | ChimeSDKMeetings | Chime | 
| Regions | multiple | US\-EAST\-1 only | 
| Endpoints | https://meetings\-chime\.region\.amazonaws\.com | https://service\.chime\.aws\.amazon\.com | 
| Service principal | meetings\.chime\.amazonaws\.com | chime\.amazonaws\.com | 
| APIs | Only APIs for meetings | APIs for meetings and other parts of Amazon Chime | 
| CreateMeeting | ExternalMeetingId and MediaRegion are required | ExternalMeetingId and MediaRegion are optional | 
| Tags | Not Available | Available | 
| Media pipelines | Available via US\-EAST\-1 endpoint | Available via US\-EAST\-1 endpoint | 
| SIP media application | JoinChimeMeeting action requires MeetingId | JoinChimeMeeting action does not require MeetingId | 
|  **Direct SIP integration**  | Not Available | Available | 

## Differences between the namespaces<a name="namespace-differences"></a>

The following sections explain the differences between the `Amazon Chime SDK` and `Amazon Chime SDK Meetings` namespaces\.

**AWS SDK namespace**  
The Amazon Chime SDK namespace uses the `Chime` formal name\. The Amazon Chime SDK Meetings namespace uses the `ChimeSDKMeetings` formal name\. The precise format of the name varies by platform\.

For example, if you use the AWS SDK in Node\.js to create meetings, you use a line of code to address the namespace\.

```
const chimeMeetings = AWS.Chime();
```

To migrate to the Amazon Chime Meetings SDK, update this line of code with the new namespace and the endpoint region\.

```
const chimeMeetings = AWS.ChimeSDKMeetings({ region: "eu-central-1" });
```

**Regions**  
The [Amazon Chime](https://docs.aws.amazon.com/chime/latest/APIReference/API_Operations_Amazon_Chime.html) namespace can only address API endpoints in the US\-EAST\-1 region\. The [Amazon Chime SDK Meetings](https://docs.aws.amazon.com/chime/latest/APIReference/API_Operations_Amazon_Chime_SDK_Meetings.html) namespace can address Amazon Chime SDK meeting API endpoints in any Region they are available\. For a current list of meeting Regions, refer to [Available regions](sdk-available-regions.md) in this guide\.

**Endpoints**  
The [Amazon Chime SDK Meetings](https://docs.aws.amazon.com/chime/latest/APIReference/API_Operations_Amazon_Chime_SDK_Meetings.html) namespace uses different API endpoints than the [Amazon Chime](https://docs.aws.amazon.com/chime/latest/APIReference/API_Operations_Amazon_Chime.html) namespace\.

Only the endpoint used to create a meeting can be used to modify it\. This means a meeting created via an endpoint in EU\-CENTRAL\-1 can only be modified via EU\-CENTRAL\-1\. It also means you cannot address a meeting created via the `Chime` namespace with the `ChimeSDKMeeting` namespace in US\-EAST\-1\.

**Service principal**  
The [Amazon Chime SDK Meetings](https://docs.aws.amazon.com/chime/latest/APIReference/API_Operations_Amazon_Chime_SDK_Meetings.html) namespace uses a new service principal: `meetings.chime.amazonaws.com`\. If you have SQS, SNS, or other IAM access policies that grant access to the service, you need to update those polices to grant access to the new service principal\.

**APIs**  
The [Amazon Chime SDK Meetings](https://docs.aws.amazon.com/chime/latest/APIReference/API_Operations_Amazon_Chime_SDK_Meetings.html) namespace only contains APIs to create and manage meetings\. The [Amazon Chime](https://docs.aws.amazon.com/chime/latest/APIReference/API_Operations_Amazon_Chime.html) namespace includes APIs for meetings and other parts of the Amazon Chime service\.

**CreateMeeting required fields**  
In the Amazon Chime SDK Meetings namespace, the [CreateMeeting](https://docs.aws.amazon.com/chime/latest/APIReference/API_meeting-chime_CreateMeeting.html) and [CreateMeetingWithAttendees](https://docs.aws.amazon.com/chime/latest/APIReference/API_meeting-chime_CreateMeetingWithAttendees.html) APIs require the ExternalMeetingId and MediaRegion fields to be specified\.

**Tagging**  
A this time, the Amazon Chime SDK Meetings namespace doesn't support tags\.

**Media pipelines**  
Amazon Chime Media Pipelines work with meetings created by any meetings endpoint, with either the [Amazon Chime SDK Meetings](https://docs.aws.amazon.com/chime/latest/APIReference/API_Operations_Amazon_Chime_SDK_Meetings.html) or the [Amazon Chime](https://docs.aws.amazon.com/chime/latest/APIReference/API_Operations_Amazon_Chime.html) namespace\. Refer to [Available Regions](https://docs.aws.amazon.com/chime/latest/dg/chime-sdk-available-regions.html) in the Developer Guide for the latest list of media pipeline regions\.

**SIP media applications**  
Amazon Chime SIP Media Applications \(SMA\) work with meetings created by any meetings endpoint, with either the [Amazon Chime SDK Meetings](https://docs.aws.amazon.com/chime/latest/APIReference/API_Operations_Amazon_Chime_SDK_Meetings.html) or the [Amazon Chime](https://docs.aws.amazon.com/chime/latest/APIReference/API_Operations_Amazon_Chime.html) namespace\. When using SMA with a meeting created through the Amazon Chime SDK Meetings namespace, the [JoinChimeMeeting](https://docs.aws.amazon.com/chime/latest/dg/join-chime-meeting.html) action requires the MeetingId parameter\.