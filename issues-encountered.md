# Issues Encountered in Our Own Experience Report Submission

## Issue 1: Citation links land offset from their references

### Description
Links to citations' references are offset vertically and horizontally when entering on links to their references from the body of the text.

### How it appears to screen reader users
Taken to a few lines above the intended reference after entering on link. Usually land in the middle of the line within prior reference. After entering on link, text appears in braille only; none is spoken until you arrow up or down.

### Why it matters
Navigating to the intended reference takes longer. This is confusing because you hear/read text about the prior reference in braille. Whether or not you'll be taken to the intended reference is unpredictable.

### Possible causes
Rather than destinations being left-aligned at the beginning of references, they are positioned slightly above and are horizontally offset relative to the intended references.

### How to check
Using a screen reader, activate several different citation links. Each time, check whether text is announced immediately (if not, arrow down once), and whether the announced reference matches the citation—by number, lead author, or visual comparison.

### Suggested fix
Template maintainers should reposition citation destinations so that each link lands at the beginning of the intended reference. Authors can adjust destination coordinates manually, but this is labor-intensive and difficult to validate. Fixing the issue upstream in the LaTeX template would be more reliable and sustainable.

## Issue 2: Footnote links land offset from their footnotes

### Description
Links to footnotes are offset vertically when entering on links to footnotes from the body of the text.

### How it appears to screen reader users
Taken to a few lines above the intended footnote within the text itself after entering on link. Usually land at the start of the line within text above the intended footnote. After entering on link, text appears in braille only; none is spoken until you arrow up or down.

### Why it matters
Footnotes are meant to clarify information. If a screenreader user is not taken to the footnote text, they do not benefit from the information listed in the footnote as quickly and are instead confused trying to find the footnote text itself. Could be confused to the point they forgot what footnote they were intending to read; by the time they find it, they may forget what part of the text they were reading; domino effect in terms of extra cognitive load keeping context in memory longer until intended footnote info is found.

### Possible causes
Similar to Issue 1—destinations of links to footnotes are slightly offset from their intended footnote item.

### How to check
Refer to Issue 1

### Suggested fix
Refer to Issue 1

## Issue 3: Citation links in the links list jump to the top of the file

### Description
Unable to navigate to citations' references from the links list. This happens to the Acrobat auto-tagged version.

### How it appears to screen reader users
When entering on citations' links to their references from the links list, you're taken to the top of the file. After entering on link, text appears in braille only; none is spoken until you arrow up or down.

### Why it matters
Navigating to the correct position may increase that publication being read. May be less encouraged to read if you can't find the publication of interest. The point of using links list is to navigate to destinations faster than finding links from body.

### Possible causes
Each `<Link>` tag is nested within a `<Reference>` tag. This is now the default behavior of Acrobat's cloud auto-tagging for all links in the PDF. PDF/UA-2 specifies this structure for intra-document links, such as citations. However, it currently causes this issue in Acrobat with JAWS when links are activated from the links list.

### How to check
Using a screen reader, activate several citation links from the links list and check whether each one lands on the intended reference. If nothing is announced immediately after activating a link, arrow down once. In Acrobat's Tags panel, check whether the citation `<Link>` tags are nested within `<Reference>` tags.

### Suggested fix
Authors can drag each `<Link>` tag out of its enclosing `<Reference>` tag in Acrobat's Tags panel and then delete the now-empty `<Reference>` tags. This may fix the issue, but it requires a lot of effort and time, especially in papers with many citations. It also departs from the structure PDF/UA-2 specifies. A more sustainable fix likely needs investigation from both Adobe and screen reader vendors. Adobe could make sure that links nested within `<Reference>` tags are properly exposed to screen readers no matter how the link is activated. JAWS and other screen readers could check whether they handle this PDF/UA-2 structure correctly.

## Issue 4: Footnote links in the links list stop at the link label

### Description
Do not navigate to footnotes' text from links list. This happens to the Acrobat auto-tagged version.

### How it appears to screen reader users
Taken to link label in text, not to footnote text itself. For example, taken to "Go to footnote…" or "1" instead of actual footnote text. After entering on the link, text appears in braille and is also spoken.

### Why it matters
Footnotes are meant to clarify information, and the links list is meant to speed up navigating to links' destinations. Neither is happening in this case: navigating to footnote text takes longer, and incorporating the footnote info in to your understanding of what you are reading takes longer also.

### Possible causes
Same as Issue 3: each footnote `<Link>` tag is nested within a `<Reference>` tag.

### How to check
Refer to Issue 3

### Suggested fix
Refer to Issue 3

## Issue 5: Inconsistent citation link labels starting with a bracket (Acrobat auto-tagged PDF)

### Description
Links to some citations contain left bracket ([) as start of link label rather than the citation number. This happens only to the Acrobat auto-tagged version, not the LaTeX-generated tagged PDF.

### How it appears to screen reader users
[citation content

### Why it matters
Links are inconsistently labeled, so someone navigating from the links list with first symbol navigation might miss these if searching by letter and not by left bracket, meaning some papers may be searched less simply because of inconsistent labeling, not because of paper quality.

### Possible causes
Autotagging inaccuracy.

### How to check
In Acrobat's Tags panel, locate the <Link> tags associated with citations and examine their contents and reading order. Check whether the opening bracket is included at the beginning or end of the link label.

### Suggested fix
Authors can manually correct the affected link labels in Acrobat by adjusting the tags using the reading order tool so that each link begins with the citation number or other meaningful citation text. Similar auto-tagging errors may also be avoided by generating the tagged PDF directly from the LaTeX source (when the template provides reliable tagging support).

## Issue 6: Redundant citation link descriptions (LaTeX-generated tagged PDF)

### Description
Citation link labels' naming is redundant. This only happens to the LaTeX-generated tagged PDF.

### How it appears to screen reader users
Each citation link begins with "Go to destination cite.0@," followed by last name year (no space before year), i.e., "Go to destination cite.0@lazar2017."

### Why it matters
Visually, you can skip over "Go to destination cite.0@." This can not be done when listening to text with screenreaders; you can somewhat skim with braille in that someone reading can place their finger after the @ sign to find the citation in question. Redundant labeling makes reading the citation take longer.

### Possible causes
When tagging is enabled, the ACM LaTeX template (`acmart-tagged`) adds an alternate description to each citation link in the format "Go to destination [destination name]." Screen readers announce this description instead of the visible citation text or citation number.

### How to check
In Acrobat's Tags panel, locate several citation `<Link>` tags and open their Properties. Check whether the Alternate Description for Links field contains text such as "Go to destination cite.0@lazar2017."

### Suggested fix
This issue appears to have been addressed in the latest ACM LaTeX template (`acmart`, not `acmart-tagged`, as `acmart` has integrated tagging support) when compiled with TeX Live 2026. Citation links no longer contain the redundant alternate descriptions, so screen readers announce only the visible citation number. This behavior is consistent with PDFs compiled without tagging enabled.

However, rather than omitting the link description entirely, providing a concise and informative description that gives screen reader users some context about the cited work and to distinguish citations from footnotes—for example, "Lazar et al., 2017" may be helpful. Any such description should remain brief and avoid repeating unnecessary destination or implementation details.

## Issue 7: Redundant footnote link descriptions (LaTeX-generated tagged PDF)

### Description
Footnote link labels' naming is redundant. This only happens to the LaTeX-generated tagged PDF.

### How it appears to screen reader users
Each footnote link label begins with "Go to destination footnote*." followed by a number (likely an x coordinate depending on footnote's position), i.e., "Go to destination footnote*.142," the label for footnote 5.

### Why it matters
Visually, you can skip over "Go to destination footnote*." This can not be done when listening to text with screenreaders; you can somewhat skim with braille in that someone reading can place their finger after the "footnote*." to find the footnote in question. Redundant labeling makes reading the footnote label take longer.

### Possible causes
Same as Issue 6

### How to check
Refer to Issue 6

### Suggested fix
As with Issue 6, this issue appears to have been resolved in the latest ACM LaTeX template (`acmart`). However, when no link description is provided, screen readers announce only the visible number. Without additional context, users may not immediately know whether the number refers to a footnote, citation, or another type of link. A concise and informative description should therefore be provided, such as "Footnote 5."
