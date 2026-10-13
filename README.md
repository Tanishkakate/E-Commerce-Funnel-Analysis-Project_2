# E-Commerce-Funnel-Analysis-Project_2

# E-commerce Conversion Funnel Analysis (MySQL + Power BI)

**Business question:** Where do shoppers drop off between viewing a product and buying, and what should the product team fix first?

**Data:** eCommerce behavior data from a multi-category store (Kaggle), October 2019. I analyzed a session-level sample of about 92.5K sessions (roughly 1% of the month). Sessions were sampled whole, so every event of a chosen session is kept together.

## Tools
Python (pandas, session sampling in a Kaggle notebook), MySQL (CTEs, conditional aggregation), Power BI (2-page dashboard)

## Method
- Sampled whole sessions by hashing `user_session`, so no session was cut in half.
- Built one row per session with flags for viewed, added to cart and purchased, then calculated conversion at each stage and by category and price band.
- Rates are calculated at session level. My first category query counted events separately and returned rates above 100%, so I rebuilt it to follow each session through the funnel.
- Strict funnel = sessions with view, cart and purchase events. The order of events was not checked.

## Key findings
- 6.74% of sessions end in a purchase (6,239 of 92,526).
- Only 49.7% of sessions that add to cart go on to buy, so about half abandon.
- 55% of purchase sessions (3,432 of 6,239) have no cart event. Cart-based rates therefore understate real conversion. Apparel shows 3,819 views and 86 purchase sessions but no cart events.
- Electronics drives the business: about 56% of purchase sessions, 9.5% view-to-cart and 52.9% cart-to-purchase.
- Appliances have high traffic but weaker conversion (5.7% view-to-cart, 44.0% cart-to-purchase).
- Cart-to-purchase rises with price (about 35% under 50, about 52% above 100). This may reflect category mix, since expensive items are mostly electronics.

## Recommendations
1. Recover abandoned carts with reminders and offers.
2. Improve appliance product pages and pricing.
3. Fix and verify cart event tracking before optimizing the funnel further.

## Limitations
- One month of data and a 1% sample. Results describe this sample, not the whole store.
- Categories with few cart sessions are hidden in the table because their rates are unreliable.
- Event order within a session was not checked.

## Dashboard
![Funnel overview](<img width="1366" height="768" alt="Screenshot (304)" src="https://github.com/user-attachments/assets/662d3ab1-b774-4d26-8341-720db46c8d83" />
)
![Segments](<img width="1366" height="768" alt="Screenshot (306)" src="https://github.com/user-attachments/assets/d476cea9-61ca-4fa0-a471-5742676b40f2" />
)

## Repo contents
`python/` (session sampling) · `sql/` · `powerbi/funnel_analysis.pbix` · `screenshots/`
