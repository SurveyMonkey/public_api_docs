##Change Log

All noteworthy changes and additions made to the V3 API are listed below. For changes that are not backwards compatible, developers will be informed via email well in advance, and an adequate transition period will be put in place to insure zero downtime. If you have any questions regarding a change, please contact [api-support@surveymonkey.com](mailto: api-support@surveymonkey.com).


###March 30th, 2016


####Add Contact Search Capabilities

**Description of Changes**: Add search and search_by query parameters to contact resource list endpoints.

**Endpoints Affected**: [/contact_lists/{id}/contacts](#contact_lists-id-contacts), [/contacts](#contacts)

**Developer Actions Required**: None


####Add an Additional Scope Requirement for Response Details

**Description of Changes**: Add "View Response Details" scope, and make it a requirent for viewing response answers. Make "View Responses" scope available to all plans.

**Endpoints Affected**: [/surveys/{id}/responses/{id}/details](#surveys-id-responses-id), [/collectors/{id}/responses/{id}/details](#surveys-id-responses-id), [/surveys/{id}/responses/bulk](#surveys-id-responses-bulk), [/collectors/{id}/responses/bulk](#collectors-id-responses-bulk)

**Developer Actions Required**: Reauthorization of every user using an application that makes use of the affected endpoints.


####Provide Complete Group Info to Groups Admins

**Description of Changes**: Fix bug preventing group admins from seeing additional group information.

**Endpoints Affected**: [/groups/{id}](#groups-id)

**Developer Actions Required**: None


####Allow Adding Contact List to Email Collector Message

**Description of Changes**: Allow adding a list of contacts lists to an email collector list by passing their ids.

**Endpoints Affected**: [/collectors/{id}/messages/{id}/recipients/bulk](#collectors-id-messages-id-recipients-bulk)

**Developer Actions Required**: None



###April 13th, 2016


####Add Copying of Existing Surveys

**Description of Changes**: Allow creation of a survey using an existing survey available to the user.

**Endpoints Affected**: [/surveys](#surveys)

**Developer Actions Required**: None


####Allow Setting of Survey Custom Variables

**Description of Changes**: Allow creation, modification, and deletion of survey custom variables.

**Endpoints Affected**: [/surveys](#surveys), [/surveys/{id}](#surveys-id)

**Developer Actions Required**: None


####Enforce Contact and Response Limits

**Description of Changes**: Enforce [contact import limits](http://help.surveymonkey.com/articles/en_US/kb/Is-there-a-limit-on-the-number-of-emails-I-can-send) and [response export limits](https://www.surveymonkey.com/pricing/details/?ut_source=pricing_summary) based on a user's plan.

**Endpoints Affected**: [/contact_lists/{id}/contacts](#contact_lists-id-contacts), [/contact_lists/{id}/contacts/bulk](#contact_lists-id-contacts-bulk), [/contacts](#contacts), [/contacts/bulk](#contacts-bulk), [/surveys/{id}/responses/{id}](#surveys-id-responses-id), [/surveys/{id}/responses/bulk](#surveys-id-responses-bulk), [/surveys/{id}/responses/{id}/details](#surveys-id-responses-id-details), [/collectors/{id}/responses/{id}](#collectors-id-responses-id), [/collectors/{id}/responses/bulk](#collectors-id-responses-bulk), [/collectors/{id}/responses/{id}/details](#collectors-id-responses-id-details)

**Developer Actions Required**: None


####Add Survey Preview URL

**Description of Changes**: Provide survey preview URL as part of survey details.

**Endpoints Affected**: [/surveys/{id}](#surveys-id), [/surveys/{id}/details](#surveys-id-details)

**Developer Actions Required**: None


###April 21st, 2016


####Introduce Application Status

**Description of Changes**: Add Draft, Public, Private, and Disabled statuses to applications. More info can be found [here](#publishing-an-app).

**Endpoints Affected**: All

**Developer Actions Required**: All existing applications will be set to Draft. Applications making calls on behalf of users within the same group as the developer should be switched to Private. Applications making calls on behalf of users outside the developer's group should be switched to Public.


####Allow Setting of Response Status

**Description of Changes**: Allow modification of response_status response field.

**Endpoints Affected**: [/surveys/{id}/responses](#surveys-id-responses), [/collectors/{id}/responses](#collectors-id-responses), [/surveys/{id}/responses/{id}](#surveys-id-responses-id), [/collectors/{id}/responses/{id}](#collectors-id-responses-id)

**Developer Actions Required**: None


####Fix Inconsistent Response Status

**Description of Changes**: In some cases the list of possible response status included 'new' instead of 'partial'. Consistently return a response status that is one of 'completed’, 'partial’, 'overquota’, or 'disqualified’.

**Endpoints Affected**: [/collectors/{id}/responses](#collectors-id-responses), [/surveys/{id}/responses/{id}](#surveys-id-responses-id), [/collectors/{id}/responses/{id}](#collectors-id-responses-id), [/surveys/{id}/responses/{id}/details](#surveys-id-responses-id-details), [/collectors/{id}/responses/{id}/details](#collectors-id-responses-id-details), [/surveys/{id}/responses/bulk](#surveys-id-responses-bulk), [/collectors/{id}/responses/bulk](#collectors-id-responses-bulk)

**Developer Actions Required**: Remove any application dependencies on the 'response_status' being set to 'new'.


####Return Edit URL for Responses

**Description of Changes**: Provide 'edit_url' field for responses that can be used to edit the response by taking or retaking the survey.

**Endpoints Affected**: [/collectors/{id}/responses](#collectors-id-responses), [/surveys/{id}/responses/{id}](#surveys-id-responses-id), [/collectors/{id}/responses/{id}](#collectors-id-responses-id), [/surveys/{id}/responses/{id}/details](#surveys-id-responses-id-details), [/collectors/{id}/responses/{id}/details](#collectors-id-responses-id-details), [/surveys/{id}/responses/bulk](#surveys-id-responses-bulk), [/collectors/{id}/responses/bulk](#collectors-id-responses-bulk)

**Developer Actions Required**: None



###April 28th, 2016


####Improve Resource Pagination

**Description of Changes**: Return 'total' and 'links' fields for all resource list endpoints. 'total' represents the total number of resources items available, and 'links' includes all pagination links.

**Endpoints Affected**: All resource list endpoints.

**Developer Actions Required**: None



###May 12th, 2016


####Add Survey Navigation URLs

**Description of Changes**: Return survey navigation URLs for edit('edit_url'), collect('collect_url'), analyze('analyze_url'), and summary('summary_url'). User needs to be logged in to visit the URL.

**Endpoints Affected**: [/surveys](#surveys), [/surveys/{id}](#surveys-id), [/surveys/{id}/details](#surveys-id-details)

**Developer Actions Required**: None


####Streamline OAuth Scope Additions

**Description of Changes**: If a developer adds scopes to an app that a user has already authorized, the authorization page will highlight the additional scopes asked for.

**Endpoints Affected**: None

**Developer Actions Required**: None


####Allow for Erasing of Question Responses

**Description of Changes**: Providing the question ID and omitting the answers during a PATCH will now delete the response for the specified question.

**Endpoints Affected**: [/surveys/{id}/responses/{id}](#surveys-id-responses-id), [/collectors/{id}/responses/{id}](#collectors-id-responses-id)

**Developer Actions Required**: Remove any application dependencies that rely on the existing functionality.


####Allow for Erasing of Response Pages

**Description of Changes**: Omitting pages during a PUT will now delete the response for the omitted pages.

**Endpoints Affected**: [/surveys/{id}/responses/{id}](#surveys-id-responses-id), [/collectors/{id}/responses/{id}](#collectors-id-responses-id)

**Developer Actions Required**: Remove any application dependencies that rely on the existing functionality.



###May 24th, 2016


####Fix Webhook Subscription URL PATCH

**Description of Changes**: Allow the webhook subscription URL to be modified via PATCH.

**Endpoints Affected**: [/webhooks/{id}](#webhooks-id)

**Developer Actions Required**: None


####Provide Recipient Info in Bulk Response Dump

**Description of Changes**: Return recipient information withing the 'metadata' field for the bulk response endpoints.

**Endpoints Affected**: [/surveys/{id}/responses/bulk](#surveys-id-responses-bulk), [/collectors/{id}/responses/bulk](#collectors-id-responses-bulk)

**Developer Actions Required**: None


####Fix Inconsistent Collection Mode

**Description of Changes**: In some cases the list of possible collection modes included 'normal’, 'manual’, and 'edited’. Consistently return a collection mode that is 'default', 'preview', 'data_entry', 'survey_preview', or 'edit'.

**Endpoints Affected**: [/collectors/{id}/responses](#collectors-id-responses), [/surveys/{id}/responses/{id}](#surveys-id-responses-id), [/collectors/{id}/responses/{id}](#collectors-id-responses-id), [/surveys/{id}/responses/{id}/details](#surveys-id-responses-id-details), [/collectors/{id}/responses/{id}/details](#collectors-id-responses-id-details), [/surveys/{id}/responses/bulk](#surveys-id-responses-bulk), [/collectors/{id}/responses/bulk](#collectors-id-responses-bulk)

**Developer Actions Required**: Remove any application dependencies on the 'collection_mode' being set to 'normal’, 'manual’, or 'edited’.


####Enable Groups Access for Platinum

**Description of Changes**: Allow access to group endpoints for users with the Platinum plan.

**Endpoints Affected**: [/groups](#groups), [/groups/{id}](#groups-id), [/groups/{id}/members](#groups-id-members), [/groups/{id}/members/{id}](#groups-id-members-id)

**Developer Actions Required**: None



###June 2nd, 2016


####Fix Updating Survey Custom Variables

**Description of Changes**: Previously, modifying custom variables for a survey would completely remove the existing variables and add them as a new set of variables. This would wipe all variable values stored on the responses for that survey, and prevent the ability to modify or add variables for new responses. Moving forward, if the name of the variable is the same, the variable will not be deleted during a PATCH or PUT.

**Endpoints Affected**: [/surveys](#surveys), [/surveys/{id}](#surveys-id)

**Developer Actions Required**: None


####Update Response Endpoints

**Description of Changes**: Update all response endpoints to start with '/surveys/{id}' or '/collectors/{id}'.

**Endpoints Affected**: [/surveys/{id}/responses/{id}](#surveys-id-responses-id), [/collectors/{id}/responses/{id}](#collectors-id-responses-id), [/surveys/{id}/responses/{id}/details](#surveys-id-responses-id-details), [/collectors/{id}/responses/{id}/details](#collectors-id-responses-id-details)

**Developer Actions Required**: Update all apps currently pointing to '/responses/{id}' or '/responses/{id}/details'. The old endpoints with continue to work for the time being, and an email will be distributed to inform developers of their deprecation date.
