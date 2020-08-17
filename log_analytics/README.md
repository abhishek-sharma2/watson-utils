## Scripts to extract and analyze Watson Assistant logs
These scripts are intended to form a data pipeline for Watson Assistant log analysis.

For more information on Watson Assistant log analysis, check out the blog series "Analyzing and Improving a Watson Assistant Solution":
* [Part 1: Analytics Personas and Existing Solutions](https://medium.com/ibm-watson/analyzing-and-improving-a-watson-assistant-solution-part-1-analytics-personas-and-existing-9fbd2f0b7478)
* [Part 2: Foundational Components of Watson Assistant analysis](https://medium.com/ibm-watson/analyzing-and-improving-a-watson-assistant-solution-part-2-foundational-components-of-watson-6596518e7a28)
* [Part 3: Recipes for common analytic patterns](https://medium.com/ibm-watson/analyzing-and-improving-a-watson-assistant-solution-part-3-recipes-for-common-analytic-patterns-1edb4b1f2ef2)

# getAllLogs.py
Using a filter argument grabs a set of logs from Watson Assistant.  Specify the maximum number of log pages (`-n`) to retrieve and the maximum number of log entries per page (`-p`).

This utility uses the `list_logs` API when a workspace_id is passed, otherwise uses `list_all_logs` API which requires a language and one of `request.context.system.assistant_id`, `workspace_id`, or `request.context.metadata.deployment` in the filter (see https://cloud.ibm.com/apidocs/assistant/assistant-v1?code=python#list-log-events-in-all-workspaces)

The `filter` syntax is documented here: https://cloud.ibm.com/docs/services/assistant?topic=assistant-filter-reference#filter-reference

Example for one workspace:
```
python3 getAllLogs.py -a your_api_key -w your_workspace_id -l https://gateway.watsonplatform.net/assistant/api -c raw -n 20 -p 500 -o 10000_logs.json -f "response_timestamp>=2019-11-01,response_timestamp<2019-11-21"
```

`NSS Manual Steps`
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_nss.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-11T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_6_1595584671717""
```

`Stuck on Standby Manual Steps`
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_stuck_on_standby.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-11T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_6_1596651752946""
```

`Mobile Delivery & Repairs`
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_mobile_delivery_repairs.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-11T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_1_1596729155116""
```

`Mobile Change Address`
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_mobile_change_address.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-11T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_4_1595511668790""
```

`Reschedule Engineer`
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_reschedule_engineer.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-11T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_1_1596004460580""
```

`Mobile Billing`
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_34/discovery_dialog_logs_week_34_mobile_billing.json -f "language::en,response_timestamp>="2020-08-14T00:00:00.000Z",response_timestamp<="2020-08-17T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_1681_1587590708431""
```

`Billing TV, Broadband and Talk`
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_34/discovery_dialog_logs_week_34_billing.json -f "language::en,response_timestamp>="2020-08-14T00:00:00.000Z",response_timestamp<="2020-08-17T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_5_1595499742220""
```

`Sky Mobile ONLY`
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_sky_mobile.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-10T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_4_1595064094774""
```

`Sky Mobile - Account and Billing`
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_sky_mobile_account_and_billing.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-10T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_8_1595062745219""
```

`Sky Mobile - Device Support`
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_sky_mobile_device_support.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-10T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_5_1595064191085""
```

`Sky Mobile - Other Queries`
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_sky_mobile_other.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-10T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_7_1587724562121""
```

`Home Move:`
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_home_move.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-11T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_10_1595063242388""
```

`Broadband:`
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_broadband.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-10T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_2_1592209187024""
```

`TV On Screen Message is Yes:`
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_tv_osm.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-10T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_7_1594058592632""
```

`TV On Screen Message is No:`
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_tv_no_osm.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-10T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_4_1592209187024""
```

`Shop Join Sky:`
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_shop.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-10T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_1_1593100478254""
```

<!-- Shop Join Sky Mobile: -->
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_shop_sky_mobile.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-10T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_4_1589457362364""
```

<!-- Shop New Phone or Contract: -->
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_shop_phone_or_contract.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-10T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_3_1589457457036""
```

<!-- Handover: -->
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_handover.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-10T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_7_1587654557592""
```

<!-- Community: -->
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_community_test.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-10T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited::"node_8_1593168815473""
```

<!-- Sky ID: -->
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_sky_id.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-10T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_3_1588600305551""
```

<!-- Vulnerable Customer Check -->
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_vulnerable_customer_check.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-14T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_3_1589563930042""
```

<!-- NSS Smart Community Deflection -->
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_33/discovery_dialog_logs_week_33_vulnerable_customer_check.json -f "language::en,response_timestamp>="2020-08-07T00:00:00.000Z",response_timestamp<="2020-08-14T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a,response.output.nodes_visited:"node_7_1596813722768""
```

`Example for Disco Bot NEW`
```
python getAllLogs.py -a xn8azGVGosucuJKayLHyjGhy8tcX4galVvhLehfckcX_ -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/week_34/discovery_dialog_logs_week_34_august_14_part_3.json -f "language::en,response_timestamp>="2020-08-14T16:00:00.000Z",response_timestamp<="2020-08-15T00:00:00.000Z",request.context.system.assistant_id::0a8376ef-2e4a-4cef-8112-8a1edf67834a"
```

`DISCO BOT OLD`
```
python getAllLogs.py -a Y_-glNOYF9NWF2rQ38BH5nM-HqMv7baXNQY8pLtZYNn0 -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/discovery_dialog_logs_week_30_part_2.json -f "language::en,response_timestamp>="2020-07-20T00:00:00.000Z",response_timestamp<="2020-07-24T00:00:00.000Z",request.context.system.assistant_id::942cc1a1-38ec-437b-b369-90562d979efa"
```

`Example for Messaging Bots`
```
python getAllLogs.py -a  -l https://api.eu-de.assistant.watson.cloud.ibm.com -c raw -o ../data/discovery_dialog_logs_week_30_July_20.json -f "language::en,response_timestamp>=2020-07-10,response_timestamp<=2020-07-13,workspace_id::"
```
The Watson Assistant team has put out a similar script at https://github.com/watson-developer-cloud/community/blob/master/watson-assistant/export_logs.py

# extractConversations.py
Takes a series of logs, extracts fields for analysis, builds a Pandas dataframe, and outputs it to a CSV file.  (The `extractConversationData` method can be called directly to build a DataFrame in memory.) The output contains the most frequently analyzed Watson Assistant log fields, some new fields to augment analysis, and custom fields that you specify.

The unique conversation identifier is provided with `-c`.  Note that if a single conversation spans multiple workspaces (skills), you cannot use `conversation_id` as the unique identifier.

Custom fields are specified with `-f`.  You can specifiy multiple custom fields as a comma-separated list, for example `-f response.context.STT_CONFIDENCE,response.context.action`.

`Example for Disco:`
```
python extractConversations.py -i ../data/week_34/discovery_dialog_logs_week_34_mobile_billing.json -o ../data/week_34/discovery_dialog_logs_week_34_mobile_billing.csv -c "response.context.metadata.user_id" -f "response.context.wds_results,response.context.article_unhelpful,response.context.discovery_search_counter,response.context.communityLinkSent,response.input,response.output"
```

`Example for Disco with IP addresses:`
```
python extractConversations.py -i ../data/discovery_dialog_logs_demo.json -o ../data/discovery_dialog_logs_demo_ip_address_2.csv -c "response.context.metadata.user_id" -f "response.context.wds_results,response.context.article_unhelpful,response.context.discovery_search_counter,response.context.communityLinkSent,response.context.integrations.chat.browser_info,response.input,response.output" 
```

Example for voice-based assistants using IBM Voice Gateway:
```
python extractConversations.py -i ..data/discovery_dialog_logs_week_23.json -o ..data/discovery_dialog_logs_week_23.csv -c "request.context.vgwSessionID"
```

# ConversationAnalysisRecipes.ipynb
This notebook demonstrates several log analytic functions, starting with downloading logs (via `getAllLogs.py`) and extracting fields of interest (via `extractConversations.py`), then demonstrating basic and intermediate analytic capabilities.

# intent_heatmap.py
Takes a tab-separated file (ie exported data frame from `ConversationAnalysisRecipes.ipynb`) and builds heat maps to help visualize the intent metrics.

```
python3 intent_heatmap.py -i first-turn-stats.tsv -o intent_conf.png -s "Total" -r "Intent Confidence" -l "Intent" -t "Classifier confidence by intent"
python3 intent_heatmap.py -i first-turn-stats.tsv -o stt_conf.png -s "Total" -r "STT Confidence" -l "Intent" -t "Speech confidence by intent"
```

# Other analyses
Several other types of analysis are possible with Watson Assistant log data.  The Watson Assistant development team has released [two notebooks](https://github.com/watson-developer-cloud/assistant-improve-recommendations-notebook) which help further analyze log data:
* Measure Notebook - The Measure notebook contains a set of automated metrics that help you monitor and understand the behavior of your system. The goal is to understand where your assistant is doing well vs where it isn’t, and to focus your improvement effort to one of the problem areas identified.
* Effectiveness Notebook - The Effectiveness notebook helps you understand relative performance of each intent and entity as well as the confusion between your intents. This information helps you prioritize your improvement effort.
* The [Dialog Skill Analysis](https://medium.com/ibm-watson/announcing-dialog-skill-analysis-for-watson-assistant-83cdfb968178) helps assess your Watson Assistant intent training data for patterns before you deploy.
* [Analyze chatbot classifier performance from logs](https://medium.com/ibm-watson/analyze-chatbot-classifier-performance-from-logs-e9cf2c7ca8fd) is a blog and video demonstrating how you can take utterances from logs and convert them into training and/or testing data.
* Beware of focusing too much on training accuracy - you should measure and be concerned about blind test accuracy.  See this two-part blog series on "Why Overfitting is a Bad Idea and How to Avoid It" with [Part 1: Overfitting in General](https://medium.com/ibm-watson/why-overfitting-is-a-bad-idea-and-how-to-avoid-it-part-1-overfitting-in-general-b8a3f9ffcf66) and [Part 2: Overfitting in Virtual Assistants](https://medium.com/ibm-watson/why-overfitting-is-a-bad-idea-and-how-to-avoid-it-part-2-overfitting-in-virtual-assistants-a30f4d999adc).

