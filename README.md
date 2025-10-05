# flyover
A simple bash script client for [flightradar24](https://www.flightradar24.com)
to query for aircraft flying overhead of a city or region of interest set by
latitude/longitude and δ°.

## Features
- Fetch brief or detailed info of aircraft flying above a
  geographical region
- Handle input data in (lat,lon,r) or (lat1,lon1,lat2,lon2) custom bounds
  format
- Automatically form the region of interest, based on a geolocation search
  string (via
  [nominatim.openstreetmap.org](https://nominatim.openstreetmap.org))
- Support fetching info of specific aircraft based on Flightradar24's ID
- Output format in raw text, JSON or show via notification


## Dependencies
- `curl jq`
- `notify-send`: (optional)

In a Debian-like distro, these can be installed with:

``` shell
sudo apt install curl jq libnotify-bin
```

## Usage
Check `flyover -h`:

```console
DESCRIPTION
    A simple client for flightradar24.com. Shows info of aircrafts flying
    overhead in a [latitude ± δ, longitude ± δ] vicinity

USAGE: flyover [OPTIONS]
OPTIONS
      [-s search_str]
        Search for city/region/place
        Use quotes for multi-word queries
      [-y latitude]
        Negative for south of equator and positive for north of equator
        Range: -90 <= latitude[float] <= +90
      [-x longitude]
        Negative for west of Prime Meridian and positive for east of Prime Meridian
        Range: -180 <= longitude[float] <= +180
      [-b bounds]
        Geographic bounds of the region of interest
        Format (comma-separated): "lat1,lon1,lat2,lon2"
      [-i flight_ids]
        flightradar24 flight_ids as a comma-separated list
        In this mode, only the corresponding flight details are queried
        Note: id is flightradar24's internal id (not ICAO or other standards)
        Format example: "id1,id2,id3"
      [-r delta_deg]
        δ in degrees in scan square : [latitude ± δ, longitude ± δ]
        Note: 1° of latitude ≈ 111 km
        Range: r[float] > 0
      [-o /path/to/detailed_flights]
        Set output path for detailed info of flights (json array)
        (implies 'detailed' mode)
      [-n]
        Use notification (implies 'detailed' mode)
      [-f]
        Set mode to 'brief', only print an augmented json
      [-v log_level]
        v = 0 : No logs. Equivalent to -q
        v = 1 : Set level to error
        v = 2 : Set level to warn
        v = 3 : Set level to info (default)
        v = 4 : Set level to debug
      [-q]
        Set log level to v = 0
      [-V]
        Print version
      [-h]
        Print help message

NOTES
    - latitude/longitude should be input in decimal degrees (not DMS)
    - Either use -s (geolocation service) OR (-y,-x) but NOT both
    - Default mode of operation is 'detailed'

EXAMPLES
    flyover -s "deylaman" -r 2
    flyover -s "قلعه گبری" -r 0.5 -n -v4
    flyover -y "-27.115" -x "-109.395" -r 24.15 -o /tmp/detailed.json
    flyover -s "深圳" -qf
    flyover -i "2b1abd2f,2b1cae23"
    flyover -b "43.58,58.72,46.58,61.72"
```

## Scope
This script is an unofficial CLI client for
[flightradar24](https://www.flightradar24.com).

> [!Note]
> The script was written out of curiosity. Please do not rely on it in
> production.

## Development
- linter: `shellcheck`
- formatter: `shfmt -i 4 -bn -ci -sr`

