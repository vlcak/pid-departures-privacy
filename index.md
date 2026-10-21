---
title: Privacy policy — PID Departures
---

# Privacy policy — PID Departures

**Effective date:** 21 October 2026

PID Departures shows public transport stop and departure information for Prague Integrated Transport (PID). The app works without an account.

## Data stored on your device

Favorites and their filters/order, nearby radius and transport preferences, cached PID stop details and departure results, per-widget configurations (including source selection and background transparency), and reminder settings are stored locally in app-private storage. The app does not synchronize this data to an account or cloud profile. Clearing the app's storage or uninstalling it removes the locally stored app data.

## Location

Nearby-stop discovery uses a foreground location fix and stop coordinates already stored on your device. Distance calculations and stop selection happen on the device; coordinates are never sent to the proxy or Golemio. To retrieve departures, the app sends the selected public stop IDs, including nearby stops. The app does not label these IDs as favorites or nearby, and does not request background location.

The current fix is kept in memory while the app is running. To allow a Nearby widget to use the last foreground fix, the app also saves it in app-private preferences for up to one hour; the widget treats fixes older than 15 minutes as stale and does not use them to select stops. Location permission is optional. Favorite stops and the rest of the app remain available if permission is denied.

Optional walking-time guidance reuses a recent, permitted precise foreground location fix and the selected public boarding stop's coordinates. The calculation runs entirely on the device, uses no routing service, and sends no coordinates. It is an approximate straight-line estimate, not a walking route or a boarding guarantee.

## Network requests and service providers

To search stops and load departures, the app sends PID stop IDs and a requested time interval to its configured proxy. When a user opens trip details, it sends the selected GTFS trip ID and service date to retrieve the ordered schedule and optional vehicle progress. It does not send device coordinates, a favorite list, an account ID, or a persistent device identifier. The proxy forwards only validated stop IDs, trip IDs, dates, and time parameters to Golemio and returns an allowlisted response. The Golemio API key is held by the proxy and is not embedded in the app.

The production proxy is configured to run as a Go service in an Azure Kubernetes Service cluster in Poland Central, behind the cluster's NGINX ingress. The ingress receives the network IP address to route requests; access logging is disabled for this ingress, and the proxy uses a SHA-256 digest of the client address for rate limiting without logging raw addresses or request bodies. Public stop, departure, and trip-detail responses are cached in process memory by query parameters. The existing PostgreSQL server is used only for the shared Golemio quota schedule, not user data.

Golemio receives the proxy's stop, time-window, and trip-detail queries. See [Golemio API documentation](https://api.golemio.cz/pid/docs/openapi/), [Microsoft's privacy statement](https://privacy.microsoft.com/privacystatement), and [Golemio privacy information](https://www.golemio.cz/).

## Advertising, analytics, and notifications

The app contains no advertising, analytics, account sign-in, or cross-device tracking. Departure reminders are optional local notifications, configured per favorite line or a specific displayed connection as a one-off, daily, or selected-weekday schedule. They use Android WorkManager and timetable data; notification permission is requested only when enabling reminders. Android may defer work; reminders are best-effort and are not guaranteed live-arrival predictions. The app does not use server push or continuous background departure polling.

Home-screen widgets are configured independently and display locally cached departures with cache timestamps. A network-constrained Android WorkManager task requests departures for their configured public stop IDs about every 15 minutes and after setup/reconfiguration, including while the app is backgrounded. Nearby widgets select stops on-device using only a recent foreground location fix; the task does not request a new location or send coordinates. Android may defer widget updates; continuous refresh is not guaranteed.

## User-initiated problem reports

You can open an editable problem-report preview for a selected public stop or departure. It includes the app version, selected stop/trip/route/platform, board time range, cache freshness/timestamps, and scheduled/predicted departure times when available. No GPS coordinates, device identifiers, favorites, or logs are attached automatically. You can edit or remove the text before choosing **Share report**. Only that explicit action opens Android's share sheet; the app does not automatically upload the report or send it to a support server. The app you choose handles the shared text under its own privacy policy. Avoid adding personal information to your description.

## External maps

Choosing **Open stop/platform in maps** opens an external map application with the selected public stop/platform coordinates and label. If no map application can handle the request, the app attempts to open a Google Maps web link at those same public coordinates. This action does not request your location permission or include your device's GPS coordinates, favorites, trip history, or device identifiers. Only your explicit tap opens the external application or browser, which handles the request under its own privacy policy. Provider markers can represent the centre of a platform rather than an entrance, and are not a walking route or an accuracy guarantee.

## Changes and contact

This policy will be updated if app behavior or service providers change. For privacy questions, use the developer contact shown on the PID Departures Google Play listing.