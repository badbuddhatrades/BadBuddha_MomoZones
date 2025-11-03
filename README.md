# BadBuddha MomoZones

![Version](https://img.shields.io/badge/version-2.1.0-blue)
![Platform](https://img.shields.io/badge/platform-NinjaTrader%208-green)
![License](https://img.shields.io/badge/license-MPL%202.0-orange)
![Status](https://img.shields.io/badge/status-multi--timeframe-brightgreen)

## Overview

BadBuddha MomoZones is a **multi-timeframe momentum zone indicator** that identifies high-momentum candles from three simultaneous timeframes (10-minute, 30-minute, and 60-minute) and visualizes support/resistance zones on any chart you're viewing. These zones extend indefinitely until broken by price action, providing persistent reference levels for trading decisions.

**Key Innovation**: Unlike traditional indicators that only analyze your current chart timeframe, MomoZones analyzes 10-min, 30-min, AND 60-min data simultaneously, displaying all detected zones on whatever timeframe you're viewing - from 1-minute charts to daily charts.

## Features

### 🎯 Multi-Timeframe Analysis
- **Simultaneous Timeframe Processing**: Analyzes 10-minute, 30-minute, and 60-minute data concurrently
- **Universal Chart Compatibility**: Works on ANY chart timeframe (tick, 1-min, 5-min, daily, etc.)
- **Timeframe Labels**: Each zone clearly marked with its source timeframe (10m, 30m, 60m)
- **Independent Zone Tracking**: Each timeframe generates zones independently based on its own momentum characteristics

### 📊 Core Features
- **Momentum Detection**: Identifies high-momentum candles using body size standard deviation and volume thresholds
- **Persistent Zones**: Zones extend across the entire chart until broken by price action (no arbitrary lookback limits)
- **Color-Coded Visualization**: Zones turn green when price is above, red when below, and hidden when price is inside
- **Volume Weighting**: Zone opacity scales with volume strength for visual prioritization
- **Zone Invalidation**: Automatically removes zones after consecutive closes through them
- **Statistics Display**: Data Box shows active zone count across all three timeframes

### 🎨 Customization
- **Configurable Font Size**: Adjust zone label text size from 6 to 24 points
- **Zone Labels**: Display timeframe, volume ratio, and body size on each zone
- **Bar Coloring**: Optional bar color changes to highlight momentum bars
- **Visual Markers**: Optional dots mark zone boundaries
- **Opacity Control**: Independent min/max opacity settings for volume weighting

### 🔔 Alert System
- **Hot Bar Alerts**: Notified when new momentum zones form on any timeframe
- **Zone Break Alerts**: Alerted when zones are invalidated
- **Timeframe-Specific**: Alerts include which timeframe triggered (10m, 30m, or 60m)

## Installation

### Quick Install

1. Download `BadBuddha_MomoZones.zip` from this repository
2. Open NinjaTrader 8 Control Center
3. Select **Tools > Import > NinjaScript Add-On**
4. Browse to the downloaded file and click **Import**
5. Restart NinjaTrader 8 if prompted
6. Verify compilation: **Tools > Edit NinjaScript > Indicator** > Find `BadBuddha_MomoZones`

## Usage

### Adding to Chart

1. Open any chart in NinjaTrader (any timeframe)
2. Right-click the chart and select **Indicators**
3. Find `BadBuddha_MomoZones` in the list
4. Click **Add** to apply with default settings
5. Configure parameters as needed

### How It Works

When you load MomoZones on your chart:

1. **NinjaTrader loads 4 data series**:
   - Primary: Your chart's timeframe
   - Series 1: 10-minute data (for zone detection)
   - Series 2: 30-minute data (for zone detection)
   - Series 3: 60-minute data (for zone detection)

2. **On each bar update**:
   - When a 10-min bar closes → Checks for momentum, creates zone if detected
   - When a 30-min bar closes → Checks for momentum, creates zone if detected
   - When a 60-min bar closes → Checks for momentum, creates zone if detected
   - On your chart's bars → Updates and redraws all zones, checks for zone breaks

3. **Zone display**:
   ```
   [10m V:2.3x] ========== (10-minute zone)
   [30m V:1.8x] ========== (30-minute zone)
   [60m V:2.1x] ========== (60-minute zone)
   ```

### Interpretation

**Zone Labels**:
- `[10m V:2.3x]` - Zone from 10-minute chart, formed with 2.3× average volume
- `[30m V:1.8x]` - Zone from 30-minute chart, formed with 1.8× average volume
- `[60m V:2.1x]` - Zone from 60-minute chart, formed with 2.1× average volume

**Zone Colors**:
- **Green**: Price closed above the zone (potential support area)
- **Red**: Price closed below the zone (potential resistance area)
- **Hidden**: Price is currently inside the zone (zone active but invisible)

**Zone Behavior**:
- Zones extend from formation point to current bar
- Persist until price closes through them (if invalidation enabled)
- Multiple consecutive closes required to invalidate (default: 2)

## Parameters

### Software Info
| Parameter | Value | Description |
|-----------|-------|-------------|
| Release Date | November 03, 2025 | Initial public release |
| Indicator | BadBuddha MomoZones | Product name |
| Version | v2.0.0.0 | Current version |
| Edition | Free | License type |
| Author | BadBuddha Customs LLC | Developer |

### Update Settings
| Parameter | Default | Description |
|-----------|---------|-------------|
| Enable Update Checks | true | Check for new versions automatically |

### Core Parameters
| Parameter | Type | Default | Range | Description |
|-----------|------|---------|-------|-------------|
| **Body Average Range** | int | 6 | 1-∞ | Lookback period for body size calculation (all timeframes) |
| **Volume Average Range** | int | 60 | 1-∞ | Lookback period for volume moving average (all timeframes) |
| **Change Bar Color** | bool | true | N/A | Enable bar color changes for momentum visualization |
| **Body Standard Deviations** | double | 2.0 | 0.1-∞ | Body size multiplier threshold (higher = fewer zones) |
| **Hot Volume Threshold** | double | 2.0 | 0.1-∞ | Volume multiplier threshold (higher = fewer zones) |
| **Show Zones** | bool | true | N/A | Display support/resistance zone rectangles |
| **Show Dots** | bool | true | N/A | Display dots at zone boundaries (primary chart only) |

### Alert Parameters
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| **Enable Alerts** | bool | false | Master switch for all alert functionality |
| **Alert on Hot Bar** | bool | true | Alert when new momentum bar detected (any timeframe) |
| **Alert on Zone Test** | bool | false | Alert when price enters/tests a zone |
| **Alert on Zone Break** | bool | false | Alert when zone is invalidated/broken |

### Zone Invalidation Parameters
| Parameter | Type | Default | Range | Description |
|-----------|------|---------|-------|-------------|
| **Enable Zone Invalidation** | bool | true | N/A | Automatically remove zones when broken |
| **Consecutive Closes to Invalidate** | int | 2 | 1-5 | Number of consecutive closes through zone to invalidate |

### Volume Weighting Parameters
| Parameter | Type | Default | Range | Description |
|-----------|------|---------|-------|-------------|
| **Enable Volume Weighting** | bool | true | N/A | Scale zone opacity based on volume strength |
| **Min Zone Opacity** | int | 30 | 10-100 | Minimum opacity for low volume zones (%) |
| **Max Zone Opacity** | int | 80 | 10-100 | Maximum opacity for high volume zones (%) |

### Zone Label Parameters
| Parameter | Type | Default | Range | Description |
|-----------|------|---------|-------|-------------|
| **Show Zone Labels** | bool | true | N/A | Display text labels on zones |
| **Show Volume on Label** | bool | true | N/A | Include volume ratio (e.g., "V:2.3x") |
| **Show Body Size on Label** | bool | false | N/A | Include body size in label |
| **Label Font Size** | int | 9 | 6-24 | Font size for zone labels (points) |

## Use Cases

### Scalping on 1-Minute Chart
- See 10-min zones for short-term support/resistance
- 30-min zones for intraday structure
- 60-min zones for major levels
- Take trades off 1-min chart while respecting higher timeframe zones

### Day Trading on 5-Minute Chart
- 10-min zones: Very short-term levels
- 30-min zones: Intraday swing structure
- 60-min zones: Key daily levels
- Confluence between multiple timeframe zones = high probability areas

### Swing Trading on Daily Chart
- Still see intraday momentum zones
- Understand where institutional momentum occurred
- Plan entries/exits around zone clusters
- Filter trades based on higher timeframe structure

## Tips & Best Practices

### General Usage
- **Start with default settings** and adjust based on your instrument's characteristics
- **Context is critical**: Zones work best with other analysis (trend, structure, order flow)
- **Volume required**: Ensure your data feed includes volume data
- **Zone confluence**: Multiple zones from different timeframes clustering = high significance

### Parameter Tuning
- **Too many zones?** Increase Body Std Devs (2.5-3.0) or Hot Volume Threshold (2.5-3.0)
- **Too few zones?** Decrease Body Std Devs (1.5-1.8) or Hot Volume Threshold (1.5-1.8)
- **Zones breaking too quickly?** Increase Consecutive Closes to Invalidate (3-5)
- **Zones staying too long?** Decrease Consecutive Closes to Invalidate (1)

### Visual Customization
- **Large monitor?** Increase Label Font Size to 12-18 for better visibility
- **Crowded chart?** Decrease Label Font Size to 6-8, or disable Show Body Size on Label
- **Focus on strong zones?** Enable Volume Weighting and set Max Opacity to 90-100
- **Clean chart?** Disable Change Bar Color and Show Dots, keep only zones

### Alert Configuration
- **Start with alerts disabled** to learn the indicator's behavior
- **Enable Alert on Hot Bar** for new zone notifications
- **Use Alert on Zone Break** to know when levels are invalidated
- **Disable Alert on Zone Test** unless specifically needed (can be noisy)

## Common Issues & Solutions

### No zones appearing
- ✅ Verify data feed includes volume
- ✅ Check Body Standard Deviations isn't too high (try 2.0)
- ✅ Ensure at least 60 bars of data loaded
- ✅ Verify Show Zones is enabled

### Too many zones cluttering chart
- ✅ Increase Body Standard Deviations to 2.5-3.0
- ✅ Increase Hot Volume Threshold to 2.5-3.0
- ✅ Enable Zone Invalidation with Consecutive Closes = 2
- ✅ Reduce Label Font Size to 6-7

### Can't see zone labels
- ✅ Verify Show Zone Labels is enabled
- ✅ Labels only appear when price is outside zone
- ✅ Increase Label Font Size if too small
- ✅ Check zone opacity isn't set too low

### Zones breaking too easily
- ✅ Increase Consecutive Closes to Invalidate to 3-5
- ✅ Consider disabling Zone Invalidation for persistent zones

### Performance issues
- ✅ MomoZones loads 3 additional data series - normal on first load
- ✅ Once data is cached, performance should be smooth
- ✅ If issues persist, reduce Body Average Range to 3-4

## Data Box Statistics

When DisplayInDataBox is enabled:

- **ActiveZones**: Total number of visible zones from all three timeframes
- **BodyAvg**: Not displayed (multi-timeframe)
- **VolumeAvg**: Not displayed (multi-timeframe)

## Version History

### v2.1.0.0 (2025-11-02) - Multi-Timeframe Release
- **NEW**: Multi-timeframe support - simultaneous analysis of 10, 30, and 60-minute data
- **NEW**: Works on any chart timeframe (tick, minute, daily, etc.)
- **NEW**: Timeframe labels on zones (10m, 30m, 60m)
- **NEW**: User-configurable label font size (6-24 points)
- **CHANGED**: Zones now extend indefinitely until broken (removed lookback limit)
- **CHANGED**: Zone invalidation checks against primary chart closes
- **IMPROVED**: Alert messages include source timeframe
- **IMPROVED**: Zone labels show timeframe prefix
- **IMPROVED**: SharedServices integration for auto-updates

### v2.0.0.0 (2025-01-27)
- **NEW**: Alert system with configurable hot bar, zone test, and zone break alerts
- **NEW**: Zone invalidation logic
- **NEW**: Volume weighting for zone opacity
- **NEW**: Statistics display in Data Box
- **NEW**: Zone labels with volume ratio and body size
- **IMPROVED**: Enhanced ZoneInfo tracking
- **IMPROVED**: More granular visual controls

### v1.0.0.0 (2024-10-24)
- Initial release **based on Richard The Red's (RTR) MomoZones for ThinkorSwim**
- Momentum candle detection with body size and volume filters
- Dynamic zone drawing with color coding
- Gap-aware body calculations

## Support

For questions, issues, or feature requests:
- **Website**: https://badbuddhacustoms.com
- **GitHub**: https://github.com/badbuddhatrades/BadBuddhaCustoms
- **Issues**: https://github.com/badbuddhatrades/BadBuddhaCustoms/issues

## Credits

Original RTR Momo Zones concept by Richard The Red (RTR) Thinkscript and InarTrades for TradingView.
Multi-timeframe NinjaTrader 8 implementation by BadBuddha Customs.

## License

Copyright © 2025, BadBuddha Customs LLC
Licensed under Mozilla Public License 2.0

---

**Disclaimer**: This indicator is provided for educational and informational purposes only. Trading involves substantial risk of loss. Past performance does not guarantee future results. Always conduct your own analysis and risk management.
