

# Fieds-Extraction
How to extract fields

Extract fields
The process by which Splunk Enterprise extracts fields from event data and the results of that process, are referred to as extracted fields. Splunk Enterprise extracts a set of default fields for each event it indexes. Field extraction can take place either before event indexing (in the case of default fields and indexed fields) or after event indexing (in the case of search fields). You can also create custom fields by defining additional index-time and search-time field extractions, using search commands, the field extractor, or configuration files.

Set of events that you can base some dashboard panels on. Before you start building visualizations and constructing dashboard panels, make sure you have everything you need.
In this stage of the scenario you learn how to:
Identify the fields you need to search on and determine whether they exist or must be extracted from the data.
Use the Field Extractor to create field extractions.
Review what you are trying to do and determine which fields you need
To build a dashboard that monitors failed login attempts. You would like to have the following panels:
-A set of panels that provide counts of failed login attempts.
-A panel that lists the top hackers by a count of failed login events they are responsible for.
-A panel that shows the users targeted by a specific hacker with counts of login attempts made by the hacker for each user.
Inclined to build a profession as Splunk Developer? Then here is the blog post on 
Splunk Training Online.
Now look at your events and think about what fields you will need to make these panels.
Panel concept
How will you implement it?
Are new fields required?
Counts of failed login attempts, broken out by valid and invalid accounts.
Use a | stats count operation to get an event count.
No. We can use word searches to differentiate between valid and invalid accounts.
Top hackers
Use a | top <fieldname>operation to list the top hackers.
Yes. We can identify the hackers by the ip address in the event, so we need to extract the ip address values.
Targeted users
Design a drilldown search that runs | stats count by <fieldname> for events with a specific ip address.
Yes. We must extract the user name in each event. Also requires the ip address field mentioned above.
Locate hackers on a world map
Use the iplocation andgeostats commands to convert the ip address value for a hacker into a plotted location on a map.
No new fields other than the ip address field mentioned above.
The stats and top commands used in the example searches above are examples of transforming commands. You use transforming commands to display statistical information in the form of tables, charts, and visualizations.
See if the fields you need are already being extracted
The search sourcetype=secure failed, look at the fields sidebar. The fields sidebar displays two categories of extracted fields: Selected Fields and Interesting Fields. It does not always display every field that Splunk Enterprise has selected for the search.

There do not appear to be any fields that would have ip address or username values.
Click All Fields. This opens the Select Fields dialog, where you can see detail information about all of the fields extracted for this search, not just the ones that are selected or which Splunk Enterprise finds interesting.

A quick review of the Select Fields dialog proves that ip address and user name fields are not being extracted from these events. You have to extract these fields.
Click Extract New Fields in the Select Fields dialog to open the field extractor.
Step 3: Field extraction – Select a sample event
The field extractor opens on the Select Sample step, where you select a sample event for field extraction.

The field extractor indicates that you are extracting fields for the secure source type. All field extractions created by the field extractor must be associated with a source type. In this case the field extractor obtained the source type from your search. If your search did not contain a source type, you would have to provide one when you entered the field extractor.
-Click on an event to select it.
It appears as white text over a blue background in the middle of the screen.
-Click Next to select the fields that you want to extract from the event.
Field extractions can also be associated with specific host and source values, but the field extractor only enables source type field extractions. Go here for more information about field extractions and field extraction configuration.
Field extraction – Select the fields that you want to extract
On the Select Fields step of the field extractor you highlight values in the sample event for the fields that you want to extract. You can extract multiple fields from the same event.
Highlight the word root and indicate that it is a sample value of a new field called username.
Click Add Extraction.
When you do this, the field extractor attempts to extract the field from the sample events. You can see the results in the preview table near the bottom of the page. The extracted values for the field get highlighting in the same color as the value in the sample event.
 Highlight the ip address in the event as a value of a new clientip field.
Click Add Extraction again.
The preview table updates to show how the field extractor finds and extracts values for this second field.
After you have added both field extractions, your preview table should look something like this.

It appears that the fields have been extracted correctly.
Click Next to validate your field extractions and save them.
Validate and save your field extractions
On the Validate Fields step of the field extractor you can validate your field extractions. You can investigate your field extraction success by toggling to the Matches and Non-Matches views, or by viewing the tabs that have been created for the username and clientip fields.
On this page you should not find errors, but if you do you can try to fix it by removing values in events that have been incorrectly highlighted.

Click Next to save the field extraction.
This extraction pulls out both fields.
On the Save page the only thing you need to do is change Permissions to All apps.
If you keep the default value of Owner, the other dashboards you create with them will only work for you.
You are given an opportunity to set permissions for the extraction by role. For now just leave it at the default of read access for Everyone and write access for Admin.
 Click Finish to save your extractions.


