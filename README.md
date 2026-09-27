# ADSBx receiver archive (2026-09-27)

Data pulled from the SD card of a Raspberry Pi running the ADS-B Exchange (adsbx) image with readsb, tar1090 and graphs1090. The receiver was also feeding adsb.fi and OpenSky.

## graphs1090/

These are the graphs1090 / collectd RRD databases, which hold the receiver's statistics over time (Dec 2024 to Feb 2025):

- `localhost.tar.gz` is the most recent full set.
- `auto-backup-YYYY-week_NN.tar.gz` are the weekly snapshots graphs1090 made itself.

Each tarball unpacks to `localhost/`. The folders inside it:

| Folder | Contents |
|---|---|
| `dump1090-localhost` | aircraft counts, message rates, range, signal and noise, tracks, CPU used by the decoder |
| `system_stats`, `aggregation-cpu-average` | Pi temperature and CPU |
| `df-root`, `disk-mmcblk0` | SD card usage and I/O |
| `interface-eth0`, `interface-wlan0` | network traffic |

**Restore** by copying `localhost/` into `/var/lib/collectd/rrd/` on a graphs1090 install and restarting collectd. You can also read the files with `rrdtool fetch` or `rrdtool dump`.

There is no per-aircraft track history. readsb was not set up to save it: no `--write-globe-history` and no `--heatmap`.

## system/

This folder holds the receiver configs (`boot/`, `etc/default/`, `etc/collectd/`, `home/pi/adsbexchange/`) and system logs (`var/log/`).

## Removed or redacted

- **Removed:** the Wi-Fi config, the Grafana database, and the binary login records (`wtmp`, `btmp`, `lastlog`, `faillog`).
- **Redacted:** feeder UUIDs, feeder usernames, MAC addresses, LAN IPs, and login usernames in the logs.
- **Converted:** compressed logs were decompressed to plain text.
