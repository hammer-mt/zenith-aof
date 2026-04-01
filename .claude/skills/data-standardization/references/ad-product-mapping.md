# Ad Product Mapping Reference

Maps vendor-specific ad format names to MDI Ad_Product categories.

## MDI Ad_Product Categories

| Category | Description |
|----------|-------------|
| Standard_Display | Static image ads, carousels, banner ads, rich media display |
| Video | Video ads across all placements (in-feed, pre-roll, in-stream, stories) |
| Native | Dynamic product ads, native placements, discovery/content ads |
| Search | Search ads, responsive search ads, text ads |
| Shopping | Product listing ads, shopping campaigns |

## Meta Format Mapping

| Meta Format | MDI Ad_Product | Notes |
|-------------|---------------|-------|
| Single Image | Standard_Display | Standard static ad unit |
| Carousel | Standard_Display | Multi-image display format |
| Video | Video | Direct mapping |
| Dynamic Product | Native | Personalized/dynamic creative |
| Stories (Image) | Standard_Display | Story-specific static placement |
| Stories (Video) | Video | Story-specific video placement |
| Reels | Video | Short-form video |
| Collection | Native | Shopping-oriented dynamic format |
| Instant Experience | Native | Full-screen interactive format |
| Lead Form | Standard_Display | In-platform lead capture |

## Google Ads Format Mapping

| Google Ad Type | MDI Ad_Product | Notes |
|----------------|---------------|-------|
| Responsive Search | Search | Standard Google search format |
| Shopping | Shopping | Product listing ads |
| PMAX | Standard_Display | Multi-format -- always flag for review |
| Responsive Display | Standard_Display | Display network ads |
| Video (YouTube) | Video | YouTube in-stream/bumper |
| Discovery | Native | Gmail/Discover feed ads |
| App | Standard_Display | App install campaigns -- flag if not in MDI |
| Demand Gen | Standard_Display | Multi-format like PMAX -- flag for review |

## TikTok Format Mapping

| TikTok Promotion Type | MDI Ad_Product | Notes |
|------------------------|---------------|-------|
| In-Feed Video | Video | Standard TikTok ad unit |
| TopView | Video | Premium placement -- consider flagging |
| Spark Ads | Video | Boosted organic -- treated as video |
| Branded Hashtag | Video | Awareness play -- consider flagging |
| Branded Effect | Video | AR/filter format -- consider flagging |
| Search Ads | Search | TikTok search placement |

## DV360 Format Mapping

| DV360 Format | MDI Ad_Product | Notes |
|--------------|---------------|-------|
| Display | Standard_Display | Programmatic display |
| Video (Pre-roll) | Video | YouTube/web video |
| Native | Native | Programmatic native |
| Audio | Video | Audio ads -- map to Video or flag |
| CTV | Video | Connected TV -- map to Video or create new category |

## Edge Cases and Recommendations

1. **PMAX / Performance Max**: Spans Search, Display, YouTube, Discover, Shopping. No single MDI category covers it. Default to Standard_Display but always flag. Recommend adding "PMAX" or "Multi_Format" to MDI schema.

2. **TopView / Takeover ads**: These are premium awareness placements that behave differently from standard video. Consider "Premium_Video" or "Takeover" as a future MDI category.

3. **Dynamic Product Ads (DPA)**: These use product catalog data to personalize creative. Mapped to Native because the content is dynamically generated, not because of placement.

4. **Demand Gen (Google)**: Like PMAX, this spans multiple surfaces. Treat same as PMAX -- default to Standard_Display and flag.

5. **CTV / Audio**: Not currently in MDI schema. Map to Video as closest match but flag for schema expansion if these become significant spend categories.
