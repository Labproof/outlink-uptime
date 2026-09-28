# outlink uptime (outside-in check)

Every 5 minutes GitHub runs `.github/workflows/uptime.yml` against https://outlink.my from its own servers.
A failed run = something is down (checked twice, 30 s apart). **GitHub emails the repo owner when a scheduled
run fails** (Settings → Notifications → Actions: "Send notifications for failed workflows only").

Public repo on purpose: scheduled Actions are free and unlimited for public repos (a 5-minute schedule would use
~8,600 minutes a month, above the private-repo free tier). It contains no secrets, only public URLs.
The monthly keepalive commit stops GitHub pausing the schedule after 60 idle days.

The on-server monitor (`../outlink-qr-check.sh`) does the detailed checks and emails via Resend; this one
exists for the case the server can't report: the whole VPS or its network being down.
