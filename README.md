# Poland housing prices – official notarial deed data, updated weekly

What apartments **really sell for** in Poland's largest cities: the median price per m² from notarial deeds in the official Real Estate Price Register (*Rejestr Cen Nieruchomości*, RCN), compared with developers' asking prices from the price lists they must publish daily on dane.gov.pl. An automated pipeline refreshes this repository every week.

In October 2026, the median apartment sold in **Warsaw** went for **15,742 PLN per m²**, in **Czestochowa** for **7,243 PLN** – according to notarial deeds, not listings.

![Map: median apartment price per m² in notarial deeds](maps/prices.png)

## Latest numbers (2026-10-26)

| City | Median deed price (PLN/m²) | Year on year | New-build deeds | Resale deeds | Developers' asking price | Asking vs new-build deeds | Deeds up to |
|---|---:|---:|---:|---:|---:|---:|---|
| Warsaw | 15,742 | +1.7% | 15,165 | 16,385 | 17,251 | +13.8% | May 2026 |
| Krakow | 14,961 | +4.0% | 15,000 | 14,872 | 15,716 | +4.8% | September 2026 |
| Wroclaw | 12,862 | +3.5% | 13,087 | 12,669 | 15,250 | +16.5% | August 2026 |
| Gdansk | 12,622 | +6.5% | 11,938 | 13,111 | 15,656 | +31.1% | January 2026 |
| Gdynia | 11,936 | +2.7% | 12,358 | 11,702 | 13,400 | +8.4% | June 2026 |
| Poznan | 11,540 | +4.1% | 11,804 | 11,337 | 13,240 | +12.2% | September 2026 |
| Szczecin | 10,561 | +9.5% | 11,505 | 9,645 | 12,120 | +5.3% | September 2026 |
| Lublin | 10,129 | +1.2% | 9,694 | 10,129 | 11,100 | – | August 2026 |
| Katowice | 10,000 | +0.4% | 11,358 | 8,174 | 12,780 | +12.5% | September 2026 |
| Bialystok | 9,937 | +5.7% | 10,178 | 9,737 | 12,950 | +27.2% | August 2026 |
| Rzeszow | 9,613 | – | 9,322 | 10,515 | 10,800 | +15.9% | September 2026 |
| Torun | 9,512 | +7.6% | 10,098 | 8,957 | 12,300 | +21.8% | June 2026 |
| Kielce | 9,483 | +5.8% | 10,245 | 8,718 | 11,150 | +8.8% | June 2026 |
| Olsztyn | 9,343 | +8.1% | 9,588 | 9,111 | 11,100 | +15.8% | August 2026 |
| Lodz | 9,250 | – | 10,034 | 7,807 | 11,500 | +14.6% | August 2026 |
| Czestochowa | 7,243 | +2.4% | 8,355 | 6,152 | 8,300 | −0.7% | September 2026 |

![Map: developers' asking prices vs new-build deeds](maps/gap.png)

## Data files

- [`data/cities.csv`](data/cities.csv) – the latest table (median, quartiles, primary vs resale, year on year, developers' asking prices and the gap)
- [`data/history/`](data/history) – a snapshot every week, so the time series grows over time

## Data for a specific address

The same official sources, for any address in Poland, through ready-made APIs (Apify Actors – also usable without code, with Excel/CSV export):

- [Transaction prices from notarial deeds](https://apify.com/kris_fili/poland-real-estate-transaction-prices) – median, quartiles, trend and the list of deeds around any address
- [Apartment valuation (AVM)](https://apify.com/kris_fili/poland-apartment-valuation) – an estimated value for any apartment from comparable deeds
- [New-build prices](https://apify.com/kris_fili/poland-new-build-apartment-prices) – every developer offer around an address
- [Asking vs transaction price gap](https://apify.com/kris_fili/poland-housing-price-gap) – both sources compared for any location

## Use it from an AI assistant (MCP)

Add this remote MCP server to Claude, ChatGPT, Cursor or any other MCP client – it gives the assistant the four tools above (on first use you sign in with an Apify account, free tier available):

```json
{
  "mcpServers": {
    "poland-housing": {
      "url": "https://mcp.apify.com?tools=kris_fili/poland-apartment-valuation,kris_fili/poland-real-estate-transaction-prices,kris_fili/poland-new-build-apartment-prices,kris_fili/poland-housing-price-gap"
    }
  }
}
```

Then ask, for example: *"How much is a 54 m² two-room flat at Długa 12 in Kraków worth? Use notarial deed prices."*

Prefer a local server (stdio, `uvx`)? See [poland-housing-mcp](https://github.com/yngzty4229-art/poland-housing-mcp).

## Methodology

- **Deeds:** apartment sales from the RCN register (GUGiK bulk export + live web service), market sales of full ownership only, implausible prices and outliers removed.
- **12-month window** ending at the latest deed published for each city – counties publish with different delays (see the last column).
- **Year on year:** median of the last 12 months vs the 12 months before, shown only when both periods have comparable coverage.
- **Asking prices:** available apartments in developers' official daily price lists, whole city.
- New-build deeds are often signed at handover, so they reflect older price lists – part of the gap is timing.

## Sources and license

Source data: Rejestr Cen Nieruchomości – Główny Urząd Geodezji i Kartografii (public register, free since 13 Feb 2026); developers' price lists – dane.gov.pl. Voivodeship borders: PRG (GUGiK). The tables and maps in this repository are licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) – please credit "Poland housing prices, github.com/yngzty4229-art/poland-housing-prices".

---

### Po polsku

**Ceny transakcyjne mieszkań w największych miastach Polski – z aktów notarialnych, aktualizowane co tydzień.** Mediana ceny za m² z Rejestru Cen Nieruchomości (RCN) w 17 miastach, rynek pierwotny i wtórny, zmiana rok do roku oraz ceny ofertowe z cenników deweloperów (dane.gov.pl) i różnica między nimi. Dane w pliku [`data/cities.csv`](data/cities.csv), co tydzień nowy zrzut w [`data/history/`](data/history). Dane dla konkretnego adresu i wycena mieszkania: [apify.com/kris_fili](https://apify.com/kris_fili).
