---
title: Privacy policy — PID Departures
---

# Privacy policy — PID Departures

**Effective date:** 19 October 2026

PID Departures shows public transport stop and departure information for Prague Integrated Transport (PID). The app works without an account.

## Data stored on your device

Favorites and their filters/order, source and radius preferences, cached PID stop details and departure results, widget configurations, and reminder settings are stored locally in app-private storage. The app does not synchronize this data to an account or cloud profile. Clearing the app's storage or uninstalling it removes the locally stored app data.

## Location

Nearby-stop discovery uses a foreground location fix and stop coordinates already stored on your device. Distance calculations happen on the device; neither coordinates nor a derived nearby-stop list are sent to the proxy or Golemio. The app does not request background location.

The current fix is kept in memory while the app is running. To allow a Nearby widget to use the last foreground fix, the app also saves it in app-private preferences for up to one hour; the widget treats fixes older than 15 minutes as stale and does not use them to select stops. Location permission is optional. Favorite stops and the rest of the app remain available if permission is denied.

## Network requests and service providers

To search stops and load departures, the app sends PID stop IDs and a requested time interval to its configured proxy. It does not send device coordinates, a favorite list, an account ID, or a persistent device identifier. The proxy forwards only the stop and time parameters needed to Golemio and returns an allowlisted response. The Golemio API key is held by the proxy and is not embedded in the app.

The production proxy is configured to run as a Go service in an Azure Kubernetes Service cluster in Poland Central, behind the cluster's NGINX ingress. The ingress receives the network IP address to route requests; access logging is disabled for this ingress, and the proxy uses a SHA-256 digest of the client address for rate limiting without logging raw addresses or request bodies. Public stop and departure responses are cached in process memory by query parameters. The existing PostgreSQL server is used only for the shared Golemio quota schedule, not user data.

Golemio receives the proxy's stop and time-window query. See [Golemio API documentation](https://api.golemio.cz/pid/docs/openapi/), [Microsoft's privacy statement](https://privacy.microsoft.com/privacystatement), and [Golemio privacy information](https://www.golemio.cz/).

## Advertising, analytics, and notifications

The app contains no advertising, analytics, account sign-in, or cross-device tracking. Departure reminders are optional local notifications, configured per favorite line and scheduled from timetable data using Android WorkManager. Notification permission is requested only when enabling reminders. Android may defer work; reminders are best-effort and are not guaranteed live-arrival predictions. The app does not use server push or continuous background departure polling.

Home-screen widgets are configured independently and display locally cached departures. Widget updates follow Android's permitted refresh behavior and are not guaranteed to be continuous.

## Changes and contact

This policy will be updated if app behavior or service providers change. For privacy questions, use the developer contact shown on the PID Departures Google Play listing.
