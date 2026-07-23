## Email on Destination Workaround

### ﻿Alyson on Jul 25 at 3:38 PM:

Hi Karen,

TL;DR: it’s fixable using Acrobat but hard; this is likely an issue from LaTeX-to-PDF conversion rather than tagging.

When a PDF is compiled, each item in the reference list is assigned an anchor for the inline citation to target to. But in PDF the anchor isn’t directly bonded to the reference item, but rather visually where it is (I also just learned this ridiculous fact…). The screen reader would then pick up the nearest element by this visual anchor. For your paper, likely the page layout slightly shifted after the anchors were set during the PDF compilation. So even though visually all citations still go to the right reference, the screen reader picks up the previous reference because of several pixels of misalignment of the anchor. I compiled a new untagged PDF from the LaTeX files you sent me using VoiceOver, and still had the problem you mentioned. I also experimented with some tweaks to the LaTeX files but I still haven't found the cause of this. 

While using Acrobat can override anchor positions, it’s a strange way and the outcome cannot be verified without a screen reader, and it has to be done for every reference (not citation) that has this issue:

1. Go to the destinations panel
2. Navigate to the idea spot to place the destination: the top-left corner of the PDF view will be the current spot. Horizontally, it’s best to slightly cover the first line of the reference (e.g. until the top line of letter 'E' is invisible). Vertically, it’s best to leave a little bit space left to the reference. I attached a screenshot.
3. Click Create a new destination, and give it an identifiable name.
4. Find the inline citations that link to this reference → right click → edit link → actions
5. Click "Go to a page…" from the list of existing actions (usually it’s the only one) → choose 'edit' → browse → select the named destination just added.
6. Btw, as circled in the screenshot, make sure to stay on the same page when choosing the spot (step 2). For example, if the reference is on the bottom half of page 15, either resize the window or zoom in to keep the page number (shown by Acrobat) at 15, otherwise the spot will overflow to page 16.

I really wish making citations accessible wouldn't have so many issues. I will keep looking at this when I’m free to see if I can figure out the cause or a more elegant way to fix it. For now if this solution feels overly cumbersome, maybe there could be a visually hidden statement added to the beginning of the paper saying some citations would jump to the reference right before the intended one (e.g. adding an alt text to the introduction’s heading). 

Best,
Alyson
