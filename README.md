# PrayerChart

An interactive chart of daily Islamic prayer times across a whole year, for cities worldwide.

**Live site:** https://prayerchart.com/

PrayerChart plots Fajr, Sunrise, Dhuhr, Asr, Maghrib and Isha for every day of the year on one chart, so you can see how prayer times shift with the seasons for a given city.

## Features

- **Annual chart:** all six daily times drawn as curves across the year, rendered as SVG.
- **Cities:** 8 preset cities plus 65 more in a world list, covering Africa, the Americas, Asia, Europe, the Middle East and Oceania.
- **Automatic city selection:** with no city chosen, the page picks the supported city whose current UTC offset matches the browser timezone, or is the closest to it.
- **Daylight saving time:** each city follows its local DST rule (US, EU, Australia and others), and the page shows the UTC offset in effect.
- **Ramadan highlighting:** Ramadan is shaded on the chart, using the tabular Hijri calendar with per-country offsets.
- **High-latitude handling:** where the sun never reaches the Fajr or Isha angle, the page switches to the one-seventh-of-the-night approximation.
- **Interaction:** hover over the chart to preview a date, drag to select one, and today is marked.

## Linking to a city or country

Add a city or country name to the URL after `#`. Matching ignores case, and spaces are written as `+`:

```
https://prayerchart.com/#Los+Angeles
https://prayerchart.com/#Indonesia
```

An unknown name is removed from the URL, and the page falls back to automatic selection by timezone.

## How times are calculated

All times are computed in the browser from each city's latitude, longitude and UTC offset, using standard solar position formulas (declination and equation of time).

| Prayer  | Rule |
|---------|------|
| Fajr    | Sun at the city's Fajr angle below the horizon (for example 15° in North America, 18° in most other places) |
| Sunrise | Sun at -0.833° (accounts for refraction and the sun's radius) |
| Dhuhr   | Solar noon |
| Asr     | Standard (Shafi'i) method: an object's shadow equals its length plus its noon shadow |
| Maghrib | Sunset, at -0.833° |
| Isha    | Sun at the city's Isha angle below the horizon (for example 15° in North America, 17° in most other places) |

Times are approximate and shown in 24-hour format. For the exact times used for prayer in a place, follow your local mosque or Islamic authority.

## Project structure

```
public_html/
  index.html    The whole app: markup, styles and JavaScript in one file
```

There is no build step and nothing to install. The only outside resource is Google Fonts (Playfair Display and DM Mono).

## Running locally

Open `public_html/index.html` in a browser, or serve the folder:

```
cd public_html
python3 -m http.server 8000
```

Then go to http://localhost:8000/.

## Deployment

The site is static. Serve `public_html/` as the document root of any web server.

## Author

Elfan Nofiari
