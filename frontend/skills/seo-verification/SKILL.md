---
name: seo-verification
description: Comprehensive SEO and content verification for articles and web pages. Checks on-page SEO, content quality, factual accuracy, readability, and technical SEO elements. Use after writing or updating articles to ensure search engine optimization and content veracity.
---

# SEO Verification Skill

Complete SEO audit and content verification system that checks technical SEO setup, content quality, factual accuracy, and optimization best practices.

## When to Use This Skill

Use this skill after:
- Publishing new blog posts or articles
- Updating existing content
- Creating landing pages or marketing content
- Before submitting content for review
- When optimizing content for search engines
- After making significant content changes

## Verification Workflow

### 1. Meta Data & Technical SEO Audit

**Title Tag Verification:**
```bash
# Extract and analyze title tag
curl -s "http://localhost:3000/article-url" | grep -o '<title>[^<]*</title>'
```

**Title Tag Checklist:**
- [ ] Title tag exists and is unique
- [ ] Length: 50-60 characters (ideal for SERP display)
- [ ] Includes primary keyword near the beginning
- [ ] Compelling and click-worthy
- [ ] Matches content accurately
- [ ] Brand name included (optional, at end)
- [ ] No keyword stuffing
- [ ] Proper capitalization

**Meta Description Verification:**
- [ ] Meta description exists
- [ ] Length: 150-160 characters (ideal for SERP)
- [ ] Includes primary and secondary keywords naturally
- [ ] Contains call-to-action
- [ ] Accurately summarizes content
- [ ] Unique across all pages
- [ ] Compelling for click-through

**Example Good vs Bad:**
```html
<!-- GOOD -->
<title>Complete Guide to Lice Removal: 7 Proven Methods (2026)</title>
<meta name="description" content="Discover 7 scientifically proven lice removal methods that work. Step-by-step guide with safety tips, product reviews, and expert recommendations. Read now!">

<!-- BAD -->
<title>Lice Removal Guide - Best Lice Treatment - Lice Help - Get Rid of Lice</title>
<meta name="description" content="This page is about lice removal.">
```

**Open Graph & Social Media Tags:**
- [ ] og:title present (can differ from <title>)
- [ ] og:description present
- [ ] og:image present (minimum 1200×630px)
- [ ] og:url present (canonical URL)
- [ ] og:type present (usually "article")
- [ ] twitter:card present (summary_large_image recommended)
- [ ] twitter:title present
- [ ] twitter:description present
- [ ] twitter:image present

**Example:**
```html
<meta property="og:title" content="Complete Guide to Lice Removal: 7 Proven Methods">
<meta property="og:description" content="Discover 7 scientifically proven lice removal methods...">
<meta property="og:image" content="https://example.com/images/lice-guide-social.jpg">
<meta property="og:url" content="https://example.com/guides/lice-removal">
<meta property="og:type" content="article">

<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="Complete Guide to Lice Removal: 7 Proven Methods">
<meta name="twitter:description" content="Discover 7 scientifically proven lice removal methods...">
<meta name="twitter:image" content="https://example.com/images/lice-guide-social.jpg">
```

### 2. Canonical & Indexing Verification

**Canonical Tag:**
- [ ] Canonical tag present
- [ ] Points to correct URL (self-referencing if original)
- [ ] Uses HTTPS (not HTTP)
- [ ] Absolute URL (not relative)
- [ ] No redirect chains

**Robots Meta Tag:**
- [ ] Check for `<meta name="robots" content="noindex">` (should NOT be present on published content)
- [ ] Verify indexing instructions are correct
- [ ] Check robots.txt doesn't block page

**Verification Commands:**
```bash
# Check canonical tag
curl -s "http://localhost:3000/article" | grep -i "canonical"

# Check robots meta
curl -s "http://localhost:3000/article" | grep -i 'name="robots"'

# Test robots.txt
curl -s "http://localhost:3000/robots.txt"
```

### 3. Content Structure & Heading Hierarchy

**Heading Structure Audit:**
- [ ] One and only one H1 tag
- [ ] H1 includes primary keyword
- [ ] H1 is compelling and descriptive
- [ ] Proper heading hierarchy (no skipping levels)
- [ ] H2s describe main sections
- [ ] H3s used for subsections
- [ ] Keywords naturally distributed in headings
- [ ] Headings are descriptive (not "Introduction", "Conclusion")

**Extract Heading Structure:**
```bash
# Extract all headings with hierarchy
curl -s "http://localhost:3000/article" | grep -oP '<h[1-6][^>]*>.*?</h[1-6]>' | sed 's/<[^>]*>//g'
```

**Example Good Hierarchy:**
```html
<h1>How to Remove Lice Naturally: 7 Safe Methods That Work</h1>

<h2>Understanding Head Lice: What You Need to Know</h2>
  <h3>How Lice Spread in Schools</h3>
  <h3>Common Lice Removal Myths</h3>

<h2>Method 1: Wet Combing with Conditioner</h2>
  <h3>What You'll Need</h3>
  <h3>Step-by-Step Instructions</h3>

<h2>Method 2: Essential Oil Treatment</h2>
  <h3>Best Essential Oils for Lice</h3>
  <h3>Application Instructions</h3>
```

**BAD Hierarchy (Don't Do This):**
```html
<h1>Lice Guide</h1>
<h3>Introduction</h3>  <!-- Skipped H2 -->
<h2>Methods</h2>
<h2>Method 1</h2>
<h4>Details</h4>  <!-- Skipped H3 -->
```

### 4. Keyword Optimization Analysis

**Primary Keyword Check:**
- [ ] Primary keyword identified
- [ ] Appears in: Title, H1, first 100 words, URL
- [ ] Keyword density: 1-2% (natural, not stuffed)
- [ ] Used in at least one H2
- [ ] Present in meta description
- [ ] Appears in image alt text
- [ ] Used naturally in variations/synonyms

**Secondary Keywords Check:**
- [ ] 2-4 secondary keywords identified
- [ ] Used naturally throughout content
- [ ] Appear in H2/H3 headings
- [ ] Support primary keyword

**Long-tail Keywords:**
- [ ] Include specific, question-based phrases
- [ ] Answer user intent clearly
- [ ] Featured in FAQ section if applicable

**Keyword Density Checker:**
```bash
# Count keyword occurrences (adjust keyword)
KEYWORD="lice removal"
curl -s "http://localhost:3000/article" | grep -io "$KEYWORD" | wc -l

# Get total word count
curl -s "http://localhost:3000/article" | lynx -dump -stdin | wc -w

# Calculate density: (keyword count / total words) * 100
```

**Keyword Stuffing Red Flags:**
- Keyword appears in every sentence
- Unnatural phrasing to force keywords
- Keyword density above 3%
- Same exact phrase repeated (use variations)

### 5. Content Quality Assessment

**Content Length:**
- [ ] Minimum 600 words for basic pages
- [ ] 1500-2500 words for comprehensive guides
- [ ] 2500+ words for pillar content
- [ ] Length appropriate for topic depth
- [ ] No fluff or filler content

**Readability Score:**
- [ ] Flesch Reading Ease: 60-70 (conversational)
- [ ] Grade level: 7th-8th grade for general audience
- [ ] Short sentences (average 15-20 words)
- [ ] Short paragraphs (3-4 sentences max)
- [ ] Mix of sentence lengths
- [ ] Active voice preferred (80%+)

**Readability Check (requires textstat library):**
```bash
# Install if needed
pip install textstat

# Create readability checker
cat > check_readability.py << 'EOF'
import textstat
import sys
import requests
from bs4 import BeautifulSoup

url = sys.argv[1] if len(sys.argv) > 1 else "http://localhost:3000"
response = requests.get(url)
soup = BeautifulSoup(response.text, 'html.parser')

# Extract main content (adjust selector)
content = soup.find('article') or soup.find('main') or soup.body
text = content.get_text()

print(f"Word Count: {textstat.lexicon_count(text)}")
print(f"Flesch Reading Ease: {textstat.flesch_reading_ease(text)}")
print(f"Flesch-Kincaid Grade: {textstat.flesch_kincaid_grade(text)}")
print(f"Average Sentence Length: {textstat.avg_sentence_length(text)}")
EOF

python check_readability.py "http://localhost:3000/article"
```

**Content Formatting:**
- [ ] Bullet points for lists
- [ ] Numbered lists for steps
- [ ] Bold for emphasis (not overused)
- [ ] Italics for definitions or foreign terms
- [ ] Block quotes for testimonials/quotes
- [ ] Code blocks for technical content
- [ ] Tables for data comparison
- [ ] White space between sections

**Content Structure:**
- [ ] Clear introduction (what, why, who)
- [ ] Table of contents for long articles
- [ ] Logical section flow
- [ ] Transition sentences between sections
- [ ] Summary or conclusion
- [ ] Clear call-to-action

### 6. Image Optimization

**Image SEO Checklist:**
- [ ] All images have descriptive alt text
- [ ] Alt text includes keywords naturally
- [ ] File names are descriptive (lice-removal-comb.jpg, not IMG_1234.jpg)
- [ ] Images compressed (WebP preferred)
- [ ] File size < 200KB per image
- [ ] Responsive images with srcset
- [ ] Lazy loading enabled
- [ ] Proper aspect ratios
- [ ] Images add value (not decorative only)

**Alt Text Examples:**
```html
<!-- GOOD -->
<img src="lice-removal-fine-tooth-comb.jpg"
     alt="Fine-tooth nit comb removing head lice from child's hair">

<!-- BAD -->
<img src="IMG_1234.jpg" alt="image">
<img src="comb.jpg" alt="comb comb lice comb lice removal comb">  <!-- keyword stuffing -->
<img src="photo.jpg" alt="">  <!-- empty alt -->
```

**Image Audit Commands:**
```bash
# Find images without alt text
curl -s "http://localhost:3000/article" | grep -o '<img[^>]*>' | grep -v 'alt='

# Find images with empty alt
curl -s "http://localhost:3000/article" | grep -o '<img[^>]*alt=""[^>]*>'

# List all image file names
curl -s "http://localhost:3000/article" | grep -oP 'src="[^"]*\.(jpg|png|webp|gif)"' | sed 's/src="//;s/"//'
```

### 7. Internal & External Linking

**Internal Links:**
- [ ] 3-5 internal links to related content
- [ ] Anchor text is descriptive (not "click here")
- [ ] Links to cornerstone/pillar content
- [ ] Links open in same tab
- [ ] No broken internal links
- [ ] Link to category/hub pages

**External Links:**
- [ ] Link to authoritative sources
- [ ] Citations for statistics/claims
- [ ] External links open in new tab (optional)
- [ ] Use rel="nofollow" for untrusted/sponsored links
- [ ] Check all links work (no 404s)
- [ ] Link to recent sources (within 2-3 years)

**Link Audit:**
```bash
# Extract all links
curl -s "http://localhost:3000/article" | grep -oP 'href="[^"]*"' | sed 's/href="//;s/"//' | sort | uniq

# Check for broken links (requires linkchecker)
linkchecker http://localhost:3000/article

# Or use simple curl check
for url in $(curl -s "http://localhost:3000/article" | grep -oP 'href="[^"]*"' | sed 's/href="//;s/"//'); do
  curl -s -o /dev/null -w "%{http_code} $url\n" "$url"
done
```

**Link Best Practices:**
- Link to 2-3 authoritative external sources per 1000 words
- Use exact match anchor text sparingly (looks spammy)
- Vary anchor text naturally
- Link high in the article (first 500 words)

### 8. Schema Markup (Structured Data)

**Article Schema:**
```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "How to Remove Lice Naturally: 7 Safe Methods That Work",
  "description": "Discover 7 scientifically proven lice removal methods...",
  "image": "https://example.com/images/lice-guide.jpg",
  "author": {
    "@type": "Person",
    "name": "Dr. Jane Smith"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Lice Removal Guide",
    "logo": {
      "@type": "ImageObject",
      "url": "https://example.com/logo.png"
    }
  },
  "datePublished": "2026-02-06",
  "dateModified": "2026-02-06",
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://example.com/guides/lice-removal"
  }
}
```

**FAQ Schema (for articles with questions):**
```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "How long does it take to remove lice?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Complete lice removal typically takes 2-3 weeks with consistent treatment..."
      }
    },
    {
      "@type": "Question",
      "name": "Can lice live on pillows?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Lice can survive off the human head for 24-48 hours..."
      }
    }
  ]
}
```

**How-To Schema (for step-by-step guides):**
```json
{
  "@context": "https://schema.org",
  "@type": "HowTo",
  "name": "How to Remove Lice with Wet Combing",
  "description": "Step-by-step guide to removing lice using wet combing method",
  "totalTime": "PT30M",
  "step": [
    {
      "@type": "HowToStep",
      "name": "Apply conditioner",
      "text": "Apply generous amount of conditioner to dry hair...",
      "image": "https://example.com/step1.jpg"
    },
    {
      "@type": "HowToStep",
      "name": "Comb through sections",
      "text": "Divide hair into sections and comb from roots to tips...",
      "image": "https://example.com/step2.jpg"
    }
  ]
}
```

**Schema Verification:**
```bash
# Test schema markup with Google's Rich Results Test
# (requires API access or manual testing)
echo "Test schema at: https://search.google.com/test/rich-results"

# Or extract JSON-LD schema from page
curl -s "http://localhost:3000/article" | grep -oP '<script type="application/ld\+json">.*?</script>' | sed 's/<script type="application\/ld+json">//;s/<\/script>//'
```

**Schema Checklist:**
- [ ] Schema markup present
- [ ] Valid JSON-LD format
- [ ] No syntax errors
- [ ] All required properties present
- [ ] Image URLs are absolute
- [ ] Dates in ISO 8601 format
- [ ] Tested with Google Rich Results Test

### 9. Factual Accuracy & Veracity Check

**Fact-Checking Process:**

**Step 1: Identify Claims**
- [ ] Extract all factual statements
- [ ] Identify statistics and numbers
- [ ] List all "studies show" or "research indicates" claims
- [ ] Note any medical/health claims
- [ ] Flag any "X% of people" statements

**Step 2: Verify Sources**
- [ ] Each claim has a source
- [ ] Sources are authoritative (.gov, .edu, peer-reviewed)
- [ ] Sources are recent (within 2-3 years)
- [ ] Links to sources work
- [ ] Source actually supports the claim (read it!)
- [ ] No circular citations (citing sites that cite each other)

**Step 3: Cross-Reference Information**
```bash
# Use web search to verify claims
# Example: Verify a health claim about lice
```

**Authoritative Sources by Topic:**

**Medical/Health:**
- [ ] CDC (cdc.gov)
- [ ] WHO (who.int)
- [ ] NIH (nih.gov)
- [ ] Mayo Clinic (mayoclinic.org)
- [ ] PubMed studies (pubmed.ncbi.nlm.nih.gov)
- [ ] Academic medical centers
- Avoid: Random blogs, social media, unverified sources

**Statistics:**
- [ ] Government statistical agencies
- [ ] Pew Research
- [ ] Academic research papers
- [ ] Industry reports from reputable firms
- Avoid: Infographics without sources, marketing materials

**Technical/Scientific:**
- [ ] Peer-reviewed journals
- [ ] University research
- [ ] Government research labs
- [ ] Professional organizations
- Avoid: Press releases without studies, "experts say" without names

**Step 4: Red Flags for Misinformation**
- [ ] "Studies show" without naming the study
- [ ] Outdated information (>5 years old for fast-moving topics)
- [ ] Cherry-picked data supporting only one view
- [ ] Correlation presented as causation
- [ ] Absolute statements ("always", "never", "100%")
- [ ] Sensational claims without evidence
- [ ] "Miracle cure" or "doctors hate this" language
- [ ] Anonymous experts ("experts say")

**Fact-Checking Workflow:**
```bash
# Create a fact-checking checklist
cat > fact_check.md << 'EOF'
# Fact-Checking Checklist

## Claim 1: [State the claim]
- **Source:** [URL or citation]
- **Source Type:** [Government/Academic/News/Other]
- **Date:** [Publication date]
- **Verified:** [Yes/No/Partially]
- **Notes:** [Any caveats or context]

## Claim 2: [State the claim]
- **Source:** [URL or citation]
- **Source Type:** [Government/Academic/News/Other]
- **Date:** [Publication date]
- **Verified:** [Yes/No/Partially]
- **Notes:** [Any caveats or context]

[Continue for all claims...]

## Overall Veracity: [High/Medium/Low]
## Action Items:
- [ ] Update claim X with newer data
- [ ] Add source for claim Y
- [ ] Remove unverified claim Z
EOF
```

**Verification Using Web Search:**
For each factual claim, verify using:
1. Search the exact claim on Google
2. Add site:gov or site:edu to search
3. Check multiple authoritative sources agree
4. Verify the date of the information
5. Read the actual source (not just headlines)

**Example Verification Process:**
```
Claim: "Head lice affect 6-12 million children per year in the United States"

Verification Steps:
1. Search: "head lice statistics United States CDC"
2. Find CDC source: https://www.cdc.gov/parasites/lice/head/gen_info/faqs.html
3. Verify exact number: CDC says "6 to 12 million infestations"
4. Check date: Information current as of 2024
5. Cross-reference: Mayo Clinic confirms similar range
6. Result: ✅ VERIFIED with authoritative source
```

### 10. E-E-A-T Assessment (Experience, Expertise, Authoritativeness, Trustworthiness)

**Experience Indicators:**
- [ ] Author has direct experience with topic
- [ ] Personal anecdotes or case studies included
- [ ] First-hand photos or documentation
- [ ] Practical insights beyond theory
- [ ] Detailed "how-to" based on real application

**Expertise Indicators:**
- [ ] Author credentials displayed
- [ ] Author bio with relevant qualifications
- [ ] References to professional experience
- [ ] Technical accuracy and depth
- [ ] Links to author's other work

**Authoritativeness Indicators:**
- [ ] Author is recognized in the field
- [ ] Content cited by other sites
- [ ] Published on authoritative domain
- [ ] Mentions awards or recognition
- [ ] Featured in reputable publications

**Trustworthiness Indicators:**
- [ ] Clear contact information
- [ ] Privacy policy present
- [ ] Transparent about affiliations
- [ ] Discloses sponsored content
- [ ] Facts are sourced
- [ ] Professional design and maintenance
- [ ] HTTPS enabled
- [ ] No misleading ads
- [ ] Clear date published/updated
- [ ] Corrections policy (if applicable)

**Author Bio Example:**
```html
<section class="author-bio">
  <h3>About the Author</h3>
  <img src="author-photo.jpg" alt="Dr. Jane Smith">
  <p>
    <strong>Dr. Jane Smith</strong> is a board-certified pediatrician with 15 years
    of experience treating head lice infestations. She has published research on
    lice treatment efficacy in the Journal of Pediatric Medicine and serves as a
    consultant to the CDC on parasitic infections.
  </p>
  <p>
    Medical Review: This article was medically reviewed by Dr. John Doe,
    Infectious Disease Specialist.
  </p>
  <p class="last-updated">Last Updated: February 6, 2026</p>
</section>
```

### 11. Mobile & Page Speed Optimization

**Mobile-Friendly Check:**
- [ ] Responsive design works on mobile
- [ ] Text readable without zooming
- [ ] Buttons/links are tap-friendly (44×44px minimum)
- [ ] No horizontal scrolling
- [ ] Images scale properly
- [ ] Font size minimum 16px for body text

**Page Speed:**
- [ ] Load time < 3 seconds on 3G
- [ ] First Contentful Paint < 1.8s
- [ ] Largest Contentful Paint < 2.5s
- [ ] Cumulative Layout Shift < 0.1
- [ ] Images optimized and lazy-loaded
- [ ] CSS and JS minified
- [ ] No render-blocking resources

**Test Page Speed:**
```bash
# Using Lighthouse
lighthouse http://localhost:3000/article --only-categories=performance,seo,accessibility --output=html --output-path=./seo-audit.html

# Or Google PageSpeed Insights
echo "Test at: https://pagespeed.web.dev/"
```

### 12. URL Structure

**URL Best Practices:**
- [ ] Short and descriptive (3-5 words)
- [ ] Includes primary keyword
- [ ] Uses hyphens (not underscores)
- [ ] All lowercase
- [ ] No special characters or spaces
- [ ] No dynamic parameters (?id=123)
- [ ] Reflects content hierarchy
- [ ] HTTPS (not HTTP)

**Good URLs:**
```
✅ https://example.com/guides/natural-lice-removal
✅ https://example.com/blog/lice-prevention-tips
✅ https://example.com/treatments/essential-oils-for-lice
```

**Bad URLs:**
```
❌ https://example.com/page?id=12345&cat=4
❌ https://example.com/Blog_Post_About_Lice_2026
❌ https://example.com/guides/this-is-a-very-long-url-with-too-many-words-that-goes-on-forever
❌ http://example.com/article  (not HTTPS)
```

### 13. Content Freshness

**Freshness Indicators:**
- [ ] Publication date displayed
- [ ] "Last updated" date shown
- [ ] Current year mentioned in content
- [ ] Recent statistics (within 1-2 years)
- [ ] Up-to-date product recommendations
- [ ] No broken links or outdated references
- [ ] Seasonal content updated annually

**Update Strategy:**
- Review content quarterly for accuracy
- Update statistics annually
- Refresh examples and screenshots
- Add new sections for emerging trends
- Update "current year" references

### 14. Conversion Optimization (CRO)

**Call-to-Action:**
- [ ] Clear CTA present
- [ ] CTA appears above the fold
- [ ] CTA repeated at article end
- [ ] Action-oriented language ("Get", "Download", "Start")
- [ ] Contrasting button color
- [ ] Value proposition clear
- [ ] Low friction (minimal form fields)

**Lead Magnets:**
- [ ] Relevant content upgrade
- [ ] Clear benefit stated
- [ ] Easy to access
- [ ] Delivers immediate value

**Examples:**
```html
<!-- CTA in introduction -->
<div class="cta-box">
  <h3>Get Our Free Lice Removal Checklist</h3>
  <p>Download our printable 7-step checklist to eliminate lice fast.</p>
  <button>Download Free Checklist</button>
</div>

<!-- CTA in conclusion -->
<div class="cta-conclusion">
  <h3>Need Expert Help?</h3>
  <p>Schedule a free consultation with our lice removal specialists.</p>
  <a href="/contact" class="button-primary">Schedule Free Consultation</a>
</div>
```

### 15. Automated SEO Audit Script

**Complete Audit Script:**
```bash
#!/bin/bash
# save as seo-audit.sh

URL="${1:-http://localhost:3000}"
echo "🔍 Running SEO Audit for: $URL"
echo "=================================="

# Fetch the page
CONTENT=$(curl -s "$URL")

# 1. Title Tag
echo ""
echo "📌 TITLE TAG:"
echo "$CONTENT" | grep -o '<title>[^<]*</title>' | sed 's/<title>//;s/<\/title>//'
TITLE_LENGTH=$(echo "$CONTENT" | grep -o '<title>[^<]*</title>' | sed 's/<title>//;s/<\/title>//' | wc -c)
echo "Length: $TITLE_LENGTH characters (ideal: 50-60)"

# 2. Meta Description
echo ""
echo "📝 META DESCRIPTION:"
echo "$CONTENT" | grep -i 'name="description"' | grep -o 'content="[^"]*"' | sed 's/content="//;s/"//'
DESC_LENGTH=$(echo "$CONTENT" | grep -i 'name="description"' | grep -o 'content="[^"]*"' | sed 's/content="//;s/"//' | wc -c)
echo "Length: $DESC_LENGTH characters (ideal: 150-160)"

# 3. Heading Structure
echo ""
echo "📋 HEADING STRUCTURE:"
echo "$CONTENT" | grep -oP '<h[1-6][^>]*>.*?</h[1-6]>' | sed 's/<[^>]*>//g' | nl

# 4. H1 Count
H1_COUNT=$(echo "$CONTENT" | grep -o '<h1[^>]*>' | wc -l)
echo ""
echo "🎯 H1 COUNT: $H1_COUNT (should be exactly 1)"

# 5. Images without alt
echo ""
echo "🖼️  IMAGES WITHOUT ALT TEXT:"
echo "$CONTENT" | grep -o '<img[^>]*>' | grep -v 'alt=' | nl

# 6. Canonical Tag
echo ""
echo "🔗 CANONICAL TAG:"
echo "$CONTENT" | grep -i "canonical" | grep -o 'href="[^"]*"'

# 7. Open Graph Tags
echo ""
echo "📱 OPEN GRAPH TAGS:"
echo "$CONTENT" | grep 'property="og:' | grep -o 'content="[^"]*"'

# 8. Schema Markup
echo ""
echo "📊 SCHEMA MARKUP:"
echo "$CONTENT" | grep -c 'application/ld+json' && echo "Schema found" || echo "No schema detected"

# 9. Word Count (approximate)
echo ""
echo "📏 WORD COUNT:"
WORD_COUNT=$(echo "$CONTENT" | lynx -dump -stdin | wc -w)
echo "$WORD_COUNT words (ideal: 1500-2500 for guides)"

# 10. Links
echo ""
echo "🔗 LINK ANALYSIS:"
TOTAL_LINKS=$(echo "$CONTENT" | grep -o 'href="[^"]*"' | wc -l)
INTERNAL_LINKS=$(echo "$CONTENT" | grep -o 'href="/' | wc -l)
EXTERNAL_LINKS=$((TOTAL_LINKS - INTERNAL_LINKS))
echo "Total links: $TOTAL_LINKS"
echo "Internal: $INTERNAL_LINKS"
echo "External: $EXTERNAL_LINKS"

echo ""
echo "=================================="
echo "✅ Audit Complete"
echo "Run: lighthouse $URL --view"
echo "for detailed performance analysis"
```

**Make it executable and run:**
```bash
chmod +x seo-audit.sh
./seo-audit.sh http://localhost:3000/article
```

## SEO Verification Checklist

Use this master checklist for every article:

### Technical SEO (Must Have)
- [ ] Unique, optimized title tag (50-60 chars)
- [ ] Compelling meta description (150-160 chars)
- [ ] Canonical tag present and correct
- [ ] No noindex tag (unless intentional)
- [ ] HTTPS enabled
- [ ] Clean, keyword-rich URL
- [ ] Mobile responsive
- [ ] Page speed < 3 seconds
- [ ] Schema markup present

### Content Optimization
- [ ] 1500+ words for comprehensive content
- [ ] Single H1 with primary keyword
- [ ] Logical H2/H3 hierarchy
- [ ] Primary keyword in first 100 words
- [ ] Keyword density 1-2%
- [ ] Secondary keywords naturally used
- [ ] Images with descriptive alt text
- [ ] 3-5 internal links
- [ ] 2-3 authoritative external links

### Content Quality
- [ ] Flesch Reading Ease: 60-70
- [ ] Short paragraphs (3-4 sentences)
- [ ] Bullet points for lists
- [ ] Clear introduction and conclusion
- [ ] No spelling or grammar errors
- [ ] Original content (not duplicated)
- [ ] Value-added (not thin content)

### Fact Verification
- [ ] All statistics sourced
- [ ] Sources are authoritative
- [ ] Sources are recent (< 3 years)
- [ ] Medical claims verified with .gov/.edu
- [ ] No unsubstantiated claims
- [ ] Cross-referenced multiple sources
- [ ] Author credentials displayed

### E-E-A-T
- [ ] Author bio present
- [ ] Author expertise demonstrated
- [ ] Contact information available
- [ ] Publication date visible
- [ ] Last updated date shown
- [ ] Transparent about affiliations
- [ ] Professional presentation

### Conversion
- [ ] Clear call-to-action
- [ ] CTA above the fold
- [ ] CTA at article end
- [ ] Lead magnet offered (optional)
- [ ] Contact options available

## Tools for SEO Verification

**Free Tools:**
- Google Search Console - Index status, performance
- Google PageSpeed Insights - Performance, SEO basics
- Google Rich Results Test - Schema validation
- Google Mobile-Friendly Test - Mobile usability
- Screaming Frog (free up to 500 URLs) - Technical SEO crawl
- Hemingway Editor - Readability analysis

**Browser Extensions:**
- SEOquake - Quick on-page SEO metrics
- MozBar - Domain authority, page metrics
- META SEO inspector - Meta tag analysis
- Detailed SEO Extension - Complete on-page analysis

**Command Line:**
- curl - Fetch page source
- lynx - Text-based browser
- lighthouse - Performance & SEO audit
- linkchecker - Find broken links

## Common SEO Mistakes to Avoid

1. **Keyword Stuffing** - Using keywords unnaturally or too frequently
2. **Duplicate Content** - Copying content from other pages or sites
3. **Thin Content** - Articles with little value or depth
4. **Missing Alt Text** - Images without descriptive alt attributes
5. **Broken Links** - Links to 404 or removed pages
6. **No Mobile Optimization** - Site doesn't work well on phones
7. **Slow Load Times** - Page takes >3 seconds to load
8. **Multiple H1 Tags** - More than one H1 per page
9. **Missing Schema** - No structured data markup
10. **Outdated Information** - Content hasn't been updated in years
11. **No Sources** - Claims without citations or evidence
12. **Poor Readability** - Long paragraphs, complex sentences
13. **Generic Meta Descriptions** - Same description on multiple pages
14. **URL Parameters** - Dynamic URLs instead of clean slugs

## Post-Publication Monitoring

After publishing, monitor:

**Google Search Console:**
- [ ] Page indexed within 48 hours
- [ ] No crawl errors
- [ ] Mobile usability issues
- [ ] Core Web Vitals passing
- [ ] Rich results appearing

**Analytics (first 30 days):**
- [ ] Average time on page > 2 minutes
- [ ] Bounce rate < 70%
- [ ] Pages per session > 1
- [ ] Goal conversions tracked
- [ ] Traffic sources diversified

**Ranking Checks:**
- [ ] Track primary keyword ranking
- [ ] Monitor long-tail keyword rankings
- [ ] Check featured snippet opportunities
- [ ] Monitor competitor rankings

## Continuous Improvement

**Quarterly Content Audit:**
1. Update statistics and data
2. Refresh examples and screenshots
3. Add new sections for emerging trends
4. Update author bio
5. Check and fix broken links
6. Optimize for new keywords
7. Improve underperforming sections
8. Add more internal links from new content

**Annual Deep Refresh:**
1. Complete rewrite if >50% outdated
2. Update title and meta for better CTR
3. Add more comprehensive sections
4. Include recent case studies
5. Update all images and graphics
6. Re-optimize for evolved search intent
7. Add video or interactive content
8. Improve conversion elements

## Quick Reference: SEO Scoring

**Perfect Score (90-100):**
- All technical SEO requirements met
- High-quality, comprehensive content
- All claims verified with authoritative sources
- Strong E-E-A-T signals
- Excellent readability
- Mobile-optimized, fast loading

**Good Score (70-89):**
- Most technical requirements met
- Quality content with minor gaps
- Some unverified claims
- Adequate E-E-A-T signals
- Good readability
- Acceptable performance

**Needs Improvement (50-69):**
- Missing key technical elements
- Thin or unclear content
- Multiple unverified claims
- Weak E-E-A-T signals
- Poor readability
- Slow performance

**Failing (<50):**
- Major technical SEO issues
- Low-quality or duplicated content
- Many false or unsourced claims
- No E-E-A-T signals
- Very poor readability
- Serious performance problems
