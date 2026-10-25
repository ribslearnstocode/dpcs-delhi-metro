# Delhi NCR station coverage

Reviewed on 28 September 2026. The deployed dataset is `metro-network.json`; reproduce it with `python scripts/build_full_network.py` from the repository root. The 22-station original example is retained only in `backend/tests/fixtures/sample-network.json`.

Scope: Delhi Metro Red, Yellow, Blue (both branches), Green (both branches), Violet, Pink, Magenta (both currently separate sections), Grey and Airport Express; all 21 Noida Aqua stations; all 11 Gurugram Rapid Metro stations. Planned Golden Line and other unopened extensions are not represented as usable rail connections. The March 2026 Pink extension and Deepali Chowk–Majlis Park Magenta section are included. The unfinished gap between Krishna Park Extension and Deepali Chowk has no fabricated connection.

There are **276 distinct station records, 275 selectable station endpoints and 303 station-line states** in this model. Shared interchanges are generally one station with multiple line states. Sikandarpur's two operator stations, and stations joined by walking links, remain separate. Operator network headline totals use different interchange/branch conventions and should not be interpreted as a count of unique physical station records. Blue has 57 unique members (50 main-line + 8 branch stations minus shared Yamuna Bank). Green has 24, Pink has 46 including Soorghat, and Magenta has 33.

**Soorghat:** included in the station inventory and pass-through Pink alignment, with `status=access-unconfirmed`. The official March map counted 45 operational Pink stations. Contemporary opening reports and later passenger reports disagree about access at Soorghat, and a newer authoritative access confirmation was not found. The API therefore rejects it as a source/destination pending a documented operator update; adjacent stations remain routable. This is a stated verification limit, not a claim that its access is currently closed.

## Sources

- [DMRC March 2026 network map](https://delhimetrorail.com/static/media/DMRC-Network-Map_Jan2026_Hindi-English-13.03.2026.147097c4.pdf): network table, line coverage and named extensions. Search-indexed PDF content was available; direct download returned the site's JavaScript placeholder, so no false PDF copy is included.
- [DMRC present network](https://delhimetrorail.com/pages/about-us/present-network): corridor inventory and operational extensions.
- [Government of India, PIB, 6 March 2026](https://www.pib.gov.in/PressReleasePage.aspx?PRID=2236008&lang=1&reg=6): March 8 Pink and Magenta corridor inauguration.
- [DMRC approved Phase IV station list](https://backend.delhimetrorail.com/documents/6248/Delhi-Metro-Phases-IV-Approved-Corridors.pdf): extension station names/order; construction plans alone do not establish passenger opening.
- [NMRC official station list](https://www.nmrcnoida.com/StationList): all 21 Aqua Line stations.
- [NMRC walkway document](https://www.nmrcnoida.com/Content/pdf/NIT19122020.pdf): Sector 51/52 connection. The model promises a walking connection, not an operational air-conditioned skywalk.
- [HMRTC / Government Gazette alignment](https://hmrtc.org.in/ReadWriteData/AlignGgnFbd.pdf): Rapid Metro loop order.
- [HMRTC June 2025 DPR](https://hmrtc.org.in/ReadWriteData/RevisedFINALDPR_GurgaonMetro_June2025.pdf): Rapid Metro station inventory.
- [Legacy station-chain dataset](https://github.com/Mansehej/DelhiMetroAPI/tree/master/functions/functions/lines): factual base inventory, stored in `sources/legacy-lines`. Its old names, broken table headers, missing new stations and disconnected Pink sections were corrected by the generator; it is not accepted as a current operational authority.

## Modelling assumptions

- Ride weights: two minutes per ordinary adjacent pair; five minutes per Airport Express pair. These are explicitly estimated coursework weights, not official scheduled times or a fare model.
- Transfer weights: four minutes within a shared station, five minutes between Sikandarpur's operator stations, ten minutes for Sector 51/52 and Dhaula Kuan/South Campus walking links. Waiting, service frequency, ticket queues and live disruption are not separately modelled.
- No cost for choosing a starting line or exiting at the destination. Ordinary rail edges are bidirectional; the Rapid Metro loop is directed Phase 2 → Belvedere Towers → Cyber City → Moulsari Avenue → Phase 3 → Phase 2.
- Line branches share a line state, so changing branches is not counted as a change of metro line. A train change within the same colour may still be required operationally; this model does not infer train platforms or through-running services.
- Coordinates are hand-authored schematic anchors plus interpolation. They are not geographic survey data.
- Application search codes are unique identifiers. Old names are retained as aliases (for example HUDA City Centre and Pragati Maidan).

The dataset is marked `documented`, not `verified`: published coverage is recorded, while time weights, schematic layout and unconfirmed access remain explicit limitations. See `final_assignment_2/station_coverage/stations.csv` for the complete record-level inventory.
