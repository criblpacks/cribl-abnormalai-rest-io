# Abnormal.ai REST Collector IO
----

## About this Pack

This pack is built as a complete SOURCE + DESTINATION solution (identified by the IO suffix). Data collection and delivery happen entirely within the pack's context, eliminating the need to connect it to globally defined Sources and Destinations. 

This custom Pack is designed to collect and process Abnormal.ai data via REST API, specifically:
* [Threats](https://app.swaggerhub.com/apis/abnormal-security/abx/1.4.3#/Threats/v1_threats_retrieve)
* [Audit Logs](https://app.swaggerhub.com/apis/abnormal-security/abx/1.4.3#/Audit%20Logs/v1_auditlogs_retrieve)
* [Abuse Mailbox Messages Not Analyzed](https://app.swaggerhub.com/apis/abnormal-security/abx/1.4.3#/AI%20Security%20Mailbox%20(formerly%20known%20as%20Abuse%20Mailbox)/v1_abuse_mailbox_not_analyzed_retrieve)
* [Abuse Campaigns](https://app.swaggerhub.com/apis/abnormal-security/abx/1.4.3#/AI%20Security%20Mailbox%20(formerly%20known%20as%20Abuse%20Mailbox)/v1_abusecampaigns_retrieve)

Each data type can be configured to output data in either normalized JSON or Splunk (`_raw` + Splunk fields) format. Data is mapped to the following sourcetypes in Splunk:
* Threats: `sourcetype=abnormal:ai:threat`
* Audit Logs: `sourcetype=abnormal:ai:audit`
* Abuse Mailbox Messages Not Analyzed: `sourcetype=abnormal:ai:abuse_not_analyzed`
* Abuse Campaigns: `sourcetype=abnormal:ai:abusecampaign`

## Deployment

* This pack is configured by default to use the Worker Group's *Default Destination*.
* To use the *Default Destination*: No changes are required. The pack will route the data to the destination currently set as the Default on the Worker Group.
* To use a different Destination: You must update the pack's routes to specify your desired Destination.
* For immediate functionality without requiring Pack route filter expression modifications, every bundled Source within this pack adds a hidden field: `__packsource`. This field allows for seamless routing based on the Pack source.

### Configure the Collectors
* Obtain a `Base URL` and `API Token` from your Abnormal.ai Administrator and update the Pack variables with this information (see below for details). The credentials must have at least read access to the data listed above.
* Perform a **Commit & Deploy** (required for Preview to work) and then **Run > Preview** of each Collector to verify that they work correctly.
* Schedule the Collectors, adjusting the schedule as needed. Collectors requiring State Tracking should already have it enabled.

### Configure Output Format

Each data type can be configured to output data in either normalized JSON or Splunk (`_raw` + Splunk fields) format. Enable *only one* format for each pipeline.

### Configure your Destination/Update Pack Routes
To ensure proper data routing, you must make a choice: retain the current setting to use the Default Destination defined by your Worker Group, or define a new Destination directly inside this pack and adjust the pack's route accordingly.

### Commit and Deploy
Once everything is configured, perform a Commit & Deploy to enable data collection.

### Variables

The Pack has the following variables:
* `abnormal_base_url`: Base URL of your Abnormal.ai API endpoint
* `abnormal_api_token`: Your Abnormal.ai API token
* `abnormal_ai_default_splunk_index`: Default index for the Splunk output

## Upgrades

Upgrading certain Cribl Packs using the same Pack ID can have unintended consequences. See [Upgrading an Existing Pack](https://docs.cribl.io/stream/packs#upgrading) for details.

## Release Notes

### Version 1.0.0
- Initial release

## Contributing to the Pack

To contribute to the Pack, please connect with us on [Cribl Community Slack](https://cribl-community.slack.com/). You can suggest new features or offer to collaborate.

## License
This Pack uses the following license: [Apache 2.0](https://github.com/criblio/appscope/blob/master/LICENSE).