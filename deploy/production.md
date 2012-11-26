---
layout: default
---

# Deploy project to production

## Pingdom

We use [Pingdom](https://flatstack.basecamphq.com/W5089997) as an uptime and performance monitoring service for our production apps.

### Add new check
* [Add new check](https://my.pingdom.com/checks)
* All checks should send notifications to "FlatStack support" and to people in charge of the project.
* All checks should be of type `HTTP` or `HTTPS` unless this does not work for the endpoint.
* All checks should include "Email" as media. Include other medias (SMS, iOS, Android, etc) if you need them.

### Add new contact
* [Add new contact](https://my.pingdom.com/contacts)
* Contact should include Name and Email. Set the phone number if you need to receive SMS.


## Error handling

Use [Airbrake.io](https://flatstack.basecamphq.com/W5071773) for error handling.

## Icons

Make sure favicon is in palce.

## Error pages

Make sure all error pages styled.

## Analytics

Make sure Google Analytics is in place.

## Migrations

Make sure new migrations applyed.

## Dependencies

Make sure new application dependencies installed.
