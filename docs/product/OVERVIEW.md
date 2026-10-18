# Product overview: Chismisan

Created: 2026-10-18T22:35:00+08:00
Updated: 2026-10-18T22:35:00+08:00
Revision: 1
Status: Draft, awaiting Len's approval

> **For Claude Design:** this file is the complete product and screen spec for Chismisan.
> Generate every screen listed in [Screens](#screens) at a mobile viewport (390 x 844) and a desktop viewport (1440 x 900).
> Render each screen's listed states (loading, empty, error) as separate frames.
> Follow the [Visual design system](#visual-design-system) tokens exactly and reuse the [Shared components](#shared-components) across screens.
> The target build is plain HTML, CSS, and JavaScript with no framework, so keep components simple and CSS-friendly.

## Purpose and users

Chismisan is a small, private social feed for Len and Len's friends on campus.
It is a personal side project, not an official school product.
Only people Len invites can join, and every member sees the same shared feed.
Members post updates with text and photos, react with Like or Haha, and comment.
Success means a friend can open an invite, join, post, react, and comment without help.
Expected size is a friend group of roughly 5 to 50 members.

## Brand and tone

- **Name:** Chismisan (Filipino for "a gossip session"; the place where the chismis happens).
- **Tagline:** "Where the tea is always hot."
- **Logo:** lowercase wordmark "chismisan" in the display font, with a small steaming tea cup mark to the left.
- **Voice:** playful, friendly, casual Taglish in small doses; never mean, never corporate.
- **Examples:** "Spill the tea..." as the composer prompt, and "Ang tahimik dito... Be the first to spill the tea." for the empty feed.
- **Trademark:** do not use Facebook names, logos, colors, or the "f" mark anywhere.

## Planned capabilities and main flows

| ID | Capability | Summary |
| --- | --- | --- |
| FEAT-001 | Invite and sign-in | Join through an invite link, set a password, sign in, stay signed in, log out. |
| FEAT-002 | Profiles | Name, photo, and bio; view anyone's profile and their posts; edit your own. |
| FEAT-003 | Shared feed | All posts from all members, newest first, loaded 10 at a time. |
| FEAT-004 | Posts | Create, edit, and delete posts with text and up to 4 photos. |
| FEAT-005 | Reactions | Like or Haha on posts, one reaction per person per post, with a "who reacted" list. |
| FEAT-006 | Comments | Flat comments on a post page; authors delete their own comments. |
| FEAT-007 | Admin moderation | Len can delete any post or comment from inside the app. |

These IDs are reserved; each capability moves into its own `docs/features/FEAT-NNN-name.md` file when it is detailed for implementation.

## Scope and non-goals

**In scope for version 1:** everything in the capability table above.

**Not in version 1:**

- Friend requests or a friends list; every member sees everything.
- Direct messages, group chats, groups, events, marketplace, or stories.
- Notifications of any kind, including email, push, and in-app badges.
- Live updates; new posts and comments appear after a refresh.
- Reactions on comments, replies to comments, and editing comments.
- Reactions other than Like and Haha.
- Search, hashtags, mentions, sharing, and saving posts.
- Video, GIFs, and file attachments.
- Dark mode.
- A separate admin screen; removing a member happens in the backend dashboard.
- Self-service account deletion; members ask Len.
- Public sign-up; nobody can join without an invite.

## Platform and layout

- Web app in plain HTML, CSS, and JavaScript, mobile first, working in current Chrome, Safari, Firefox, and Edge.
- Separate HTML pages per screen so the browser Back button and shared links work.
- Single centered content column, max width 600px, with 16px side padding on mobile.
- Breakpoints to check: 375px, 768px, 1024px, 1440px; no horizontal scrolling at any width.
- On desktop the column stays centered on the page background with empty space on both sides; there are no side panels.
- A sticky top bar is on every signed-in screen; there is no bottom navigation bar.
- The backend is not chosen yet (Supabase is proposed); screens must not depend on which backend is used.

## Visual design system

Style: playful and warm, light theme, rounded cards on a soft cream background, with bold friendly type.
All color pairs below were checked for at least 4.5:1 contrast where text sits on them.

### Color tokens

| Token | Value | Use | Contrast note |
| --- | --- | --- | --- |
| `--color-primary` | `#C2410C` | Primary buttons, links, active states, logo | 5.18:1 with white text |
| `--color-primary-hover` | `#9A3412` | Primary button hover and pressed | 7.31:1 with white text |
| `--color-primary-soft` | `#FFEDD5` | Selected chips, highlighted backgrounds | Primary text on it is 4.52:1 |
| `--color-on-primary` | `#FFFFFF` | Text and icons on primary | |
| `--color-background` | `#FFF7ED` | Page background (cream) | |
| `--color-surface` | `#FFFFFF` | Cards, dialogs, top bar, inputs | |
| `--color-text` | `#1C1917` | Main text | 16.47:1 on background |
| `--color-text-muted` | `#57534E` | Timestamps, counts, helper text | 7.63:1 on white |
| `--color-placeholder` | `#78716C` | Input placeholder text | 4.8:1 on white |
| `--color-border` | `#E7E5E4` | Card borders, dividers, input borders | Decorative only |
| `--color-like` | `#1D4ED8` | Like icon and label when active | 6.7:1 on white |
| `--color-like-soft` | `#EFF6FF` | Like button background when active | |
| `--color-haha` | `#B45309` | Haha icon and label when active | 5.02:1 on white |
| `--color-haha-soft` | `#FFFBEB` | Haha button background when active | |
| `--color-danger` | `#B91C1C` | Delete actions and error text | 6.47:1 on white |
| `--color-focus` | `#C2410C` | 2px focus ring with 2px offset | |

### Typography

- Body and UI: **Nunito** (Google Fonts), weights 400, 600, 700, 800, falling back to `system-ui, sans-serif`.
- Logo and screen titles: **Fredoka** (Google Fonts), weight 600, falling back to the body font.
- Both web fonts are a proposal and need Len's approval as external resources; the system fallback must look acceptable on its own.
- Base size 16px with line height 1.5; nothing below 13px.

| Style | Size / weight | Use |
| --- | --- | --- |
| Display | 28px Fredoka 600 | Welcome and invite screen headings |
| Title | 20px Fredoka 600 | Screen titles, profile name |
| Body | 16px Nunito 400 | Post text, comments, inputs |
| Body strong | 16px Nunito 700 | Author names |
| Label | 15px Nunito 700 | Buttons |
| Meta | 13px Nunito 600 | Timestamps, "Edited", counts |

### Shape, spacing, and motion

- Spacing scale: 4, 8, 12, 16, 24, 32, 48px.
- Corner radius: 16px cards and dialogs, 12px photos and inputs, 999px pill buttons and chips, full circle avatars.
- Elevation: cards use a 1px border plus a soft shadow (`0 1px 3px rgb(28 25 23 / 0.08)`); dialogs use a stronger shadow over a 40% dark backdrop.
- Motion: 150 to 250ms ease-out for presses, dialog open, and reaction toggles; a small "pop" scale (1 to 1.15 to 1) on the reaction icon when selected.
- All non-essential motion is turned off when the user prefers reduced motion.

### Icons

- Outline SVG icons, 24px, 2px stroke, rounded caps (Lucide style); never emoji as interface icons.
- Like: thumbs up.
- Haha: a custom laughing face with closed happy eyes and an open grin, drawn in the same outline style.
- Comment: speech bubble.
- Others: camera or image (add photo), more (horizontal dots), back arrow, close (x), send (paper plane), pencil (edit), trash (delete), log out.
- Every icon-only button has a visible text label or an accessible name.

### Accessibility

- Touch targets are at least 44 x 44px with at least 8px between them.
- Visible focus ring on every interactive element; full keyboard use including dialogs (focus trapped inside, Escape closes).
- Every photo has alt text; uploaded photos default to "Photo by [name]".
- Color is never the only signal; active reactions also change their label weight and show a filled icon.
- Errors appear next to the field they belong to and are announced to screen readers.

## Shared components

| Component | Description |
| --- | --- |
| Top bar | Sticky, white, 56px tall. Left: logo (links to feed). Right: your avatar (links to your profile). On inner pages, a back arrow and page title replace the logo. |
| Avatar | Circle photo at 32, 40, or 96px; if no photo, the member's initials on a warm color chosen from their name. |
| Post card | White card: header row (avatar 40px, name, meta line "2h" plus "Edited" if edited, more button on posts you can manage), post text (long text over 6 lines collapses with "See more"), photo grid, summary row (reaction counts and comment count), action row (Like, Haha, Comment). |
| Photo grid | 1 photo: full width, aspect ratio clamped between 4:5 and 16:9. 2 photos: side by side squares. 3 photos: one large on the left, two stacked on the right. 4 photos: 2 x 2 grid. Space is reserved before images load so the layout does not jump. |
| Reaction summary | Small Like and Haha icons with their counts, e.g. "Like 3 · Haha 5"; tapping it opens the Who reacted dialog. Hidden when there are no reactions. |
| Action row | Three equal pill buttons with icon and label: Like, Haha, Comment. Active reaction uses its soft background, colored icon, and bold label. |
| Comment item | Avatar 32px, a rounded bubble with name and text, then a meta line with time and "Delete" for the author or admin. |
| Buttons | Primary (filled orange pill), Secondary (white with border), Danger (red text, or filled red inside the delete dialog), Text link. Disabled buttons are 50% opacity and not clickable. Busy buttons show a small spinner and keep their width. |
| Text input | White, 12px radius, 1px border, visible label above, helper or error text below, character counter where a limit exists. |
| Dialog | Native-style modal: full screen on mobile, centered 560px card on desktop. |
| Confirm dialog | Small centered card with title, one-line message, Cancel and a red Delete button. |
| Toast | Short message at the bottom center for 4 seconds, e.g. "Post deleted." Errors include a "Try again" action. |
| Skeleton | Gray rounded placeholder shapes in the layout of a post card, used while loading. |
| Empty state | Small illustration (steaming tea cup), one heading, one sentence, and one optional button. |
| Offline banner | Thin bar under the top bar: "You're offline. You can look around, but changes won't be saved." |

## Screens

Each screen lists its address, purpose, content, actions, and states to render.

### S-01 Welcome (`index.html` when signed out)

- **Who:** anyone who opens the site while signed out.
- **Content:** large logo, tagline, one sentence: "Chismisan is invite-only. Got an invite link? Open it to join."
- **Actions:** "Sign in" primary button for existing members.
- **Notes:** no sign-up button exists anywhere.

### S-02 Accept invite (`invite.html`)

- **Who:** a friend who opened the invite link.
- **Content:** heading "You're invited to the chismisan!", their email shown read-only, "Create password" and "Confirm password" fields (minimum 8 characters, show/hide toggle).
- **Actions:** "Join" primary button, disabled until both fields are valid.
- **States:** checking the link (spinner); invalid or used link (S-11); passwords do not match (inline error); join failed (error toast with "Try again").
- **Next:** S-03 Profile setup.

### S-03 Profile setup (`setup.html`, first sign-in only)

- **Content:** heading "Who's spilling the tea?", round photo picker with "Add photo", display name field (required, 2 to 40 characters), bio field (optional, 160 characters, counter).
- **Actions:** "Let's go" primary button (enabled once a name is entered); "Skip photo and bio for now" is implied by leaving them empty.
- **Next:** S-05 Feed.

### S-04 Sign in (`signin.html`)

- **Content:** logo, email and password fields, show/hide password toggle.
- **Actions:** "Sign in" primary button; text below: "Forgot your password? Message Len."
- **States:** signing in (busy button); wrong email or password (one inline error, "That email and password don't match."); offline (banner and disabled button).
- **Behavior:** members stay signed in on that browser until they log out.

### S-05 Feed (`index.html` when signed in)

- **Layout:** top bar; composer prompt card; list of post cards; "Load more" button at the end.
- **Composer prompt card:** your avatar, a fake input reading "Spill the tea...", and a photo button; tapping any part opens S-06.
- **States:**
  - Loading: 3 skeleton post cards.
  - Empty: tea cup illustration, "Ang tahimik dito...", "Be the first to spill the tea.", and a "Create a post" button.
  - Error: "Couldn't load the feed." with "Try again".
  - End of feed: "You're all caught up!" in place of "Load more".
  - Loading more: spinner inside the "Load more" button.
- **Actions:** react, open comments (S-07), open a profile (S-08), open a photo (S-10), open the more menu on manageable posts.

### S-06 Composer dialog (opens over the feed or profile)

- **Header:** "Cancel" on the left, title "New post" or "Edit post", "Post" or "Save" primary button on the right.
- **Body:** your avatar and name, auto-growing text area with placeholder "Spill the tea..." (2,000 characters, counter appears after 1,800), photo thumbnails each with a remove (x) button, and an "Add photos" button showing "0/4".
- **Rules:** the post button is enabled only when there is text or at least one photo; adding beyond 4 photos shows "You can add up to 4 photos."
- **States:**
  - Preparing photos: each thumbnail shows a spinner while it is shrunk.
  - Posting: "Posting..." in the button, all inputs locked, progress text "Uploading photo 2 of 3...".
  - Failed: dialog stays open with everything kept, error "Couldn't post. Your text and photos are still here." and "Try again".
  - Unsupported or unreadable file: "That file isn't a photo we can use." beside the add button.
  - Cancel with changes: confirm dialog "Discard this post?" with "Keep editing" and "Discard".
- **Edit mode:** opens with the existing text and photos; photos can be removed, added, or kept; "Save" updates the post in place and marks it "Edited".

### S-07 Post page (`post.html?id=...`)

- **Layout:** top bar with back arrow and title "Post"; the full post card (text never collapsed); comment list oldest first; comment input fixed to the bottom of the screen.
- **Comment input:** your avatar, text field "Write a comment..." (500 characters), send button enabled only when the text is not blank.
- **Behavior:** opening from the Comment button places the cursor in the comment input; a sent comment appears at the bottom and the list scrolls to it.
- **States:**
  - Loading: skeleton post and two skeleton comments.
  - No comments: "No comments yet. Start the chika!"
  - Sending: send button shows a spinner and the field is locked.
  - Send failed: the comment text stays in the field with "Couldn't send. Try again."
  - Post removed or not found: S-11 "This post was removed."

### S-08 Profile (`profile.html?id=...`)

- **Header area:** 96px avatar, display name (Title style), bio (muted; hidden if empty), "Joined October 2026".
- **Own profile actions:** "Edit profile" secondary button and "Log out" text button.
- **Below:** heading "[Name]'s posts" (or "Your posts") and their post cards, newest first, with "Load more".
- **States:** loading skeleton; no posts ("No tea spilled yet." and, on your own profile, a "Create a post" button); member not found (S-11).

### S-09 Edit profile (`edit-profile.html`)

- **Content:** large avatar with "Change photo" and "Remove photo", display name (required, 2 to 40), bio (160, counter).
- **Actions:** "Save" primary button and "Cancel".
- **States:** saving (busy button); saved (toast "Profile updated." and return to S-08); error (toast with "Try again", fields kept); leaving with unsaved changes asks "Discard changes?".

### S-10 Photo viewer (overlay)

- **Content:** dark full-screen overlay, the photo fitted to the screen, "2 / 4" counter, close (x) button.
- **Actions:** next and previous arrows on desktop and swipe on mobile; Escape or close returns to the same scroll position.

### S-11 Problem page (shared)

One layout with an illustration, heading, sentence, and a button, used for:

| Case | Heading | Sentence | Button |
| --- | --- | --- | --- |
| Invite invalid or used | "This invite doesn't work" | "It may have been used already. Ask Len for a new one." | None |
| Post removed | "This post was removed" | "The tea has gone cold." | "Back to feed" |
| Member not found | "We can't find this member" | "They may have left the chismisan." | "Back to feed" |
| Page not found | "Wala dito." | "This page doesn't exist." | "Back to feed" |

### Dialogs used across screens

- **More menu (on a post):** for your own post, "Edit post" and "Delete post"; for the admin on someone else's post, only "Delete post (admin)".
- **Confirm delete post:** "Delete this post?", "It will be gone for everyone, along with its reactions and comments.", Cancel / Delete.
- **Confirm delete comment:** "Delete this comment?", Cancel / Delete.
- **Who reacted:** tabs "All", "Like", "Haha" with counts; each row is avatar, name, and a small reaction icon; tapping a row opens that profile.
- **Discard changes:** used by the composer and edit profile.

## User flows

1. **Join:** open invite link, S-02 set password, S-03 set up profile, S-05 feed.
2. **Return visit:** open the site; if still signed in, S-05 feed; otherwise S-01, S-04, then S-05.
3. **Post:** S-05, tap "Spill the tea...", S-06 write and add photos, Post; the new post appears at the top of the feed.
4. **React:** tap Like or Haha; tapping the other switches the reaction; tapping the same one again removes it; counts update immediately and revert with an error toast if saving fails.
5. **See who reacted:** tap the reaction summary, open the Who reacted dialog, optionally open a profile.
6. **Comment:** tap Comment or the comment count, S-07 with the cursor in the input, send.
7. **Edit post:** more menu, "Edit post", S-06 in edit mode, Save; the card shows "Edited".
8. **Delete post or comment:** more menu or "Delete", confirm dialog, item disappears, toast "Post deleted." or "Comment deleted."
9. **Profiles:** tap any avatar or name to open S-08; on your own profile, "Edit profile" opens S-09.
10. **Admin:** Len sees delete options on every post and comment and uses the same confirm dialogs.
11. **Log out:** your profile, "Log out", back to S-01.

## Features and acceptance criteria

### FEAT-001 Invite and sign-in

| ID | Required behavior | Observable pass/fail criterion |
| --- | --- | --- |
| REQ-001 | Only invited people can create an account. | Visiting the site without an invite offers no way to create an account. |
| REQ-002 | A valid invite link lets the friend set a password and join. | Opening a fresh invite, entering a matching 8+ character password, and pressing Join leads to S-03. |
| REQ-003 | Used or invalid invite links are rejected. | Opening a used invite shows "This invite doesn't work" and no form. |
| REQ-004 | Members sign in with email and password. | Correct details lead to the feed; wrong details show "That email and password don't match." |
| REQ-005 | Members stay signed in until they log out. | Closing and reopening the browser shows the feed without signing in again. |
| REQ-006 | Members can log out. | After "Log out", opening the feed address shows S-01. |
| REQ-007 | Signed-out visitors cannot see member content. | Opening a post or profile address while signed out shows S-01, not the content. |

### FEAT-002 Profiles

| ID | Required behavior | Observable pass/fail criterion |
| --- | --- | --- |
| REQ-001 | First sign-in requires a display name. | S-03 cannot be submitted with an empty name or a name under 2 characters. |
| REQ-002 | Photo and bio are optional. | Submitting S-03 with only a name succeeds and shows initials as the avatar. |
| REQ-003 | Anyone signed in can view any member's profile. | Tapping a name on a post opens that member's S-08 with their posts. |
| REQ-004 | Members edit only their own profile. | "Edit profile" appears only on your own profile. |
| REQ-005 | Profile changes appear everywhere. | After changing your name, your existing posts and comments show the new name after a refresh. |
| REQ-006 | Bio is limited to 160 characters and name to 40. | Typing past the limit is blocked and the counter shows the limit. |

### FEAT-003 Shared feed

| ID | Required behavior | Observable pass/fail criterion |
| --- | --- | --- |
| REQ-001 | The feed shows every member's posts, newest first. | A post made by any member appears above older posts for all members after a refresh. |
| REQ-002 | The feed loads 10 posts at a time. | With 15 posts, the first view shows 10 and "Load more" shows the other 5. |
| REQ-003 | The end of the feed is clear. | After the last post, "You're all caught up!" appears instead of "Load more". |
| REQ-004 | Loading, empty, and error states are shown. | Each state in S-05 appears under its condition and "Try again" reloads. |
| REQ-005 | Your own new post appears without a refresh. | After posting, the new post is at the top of your feed immediately. |

### FEAT-004 Posts

| ID | Required behavior | Observable pass/fail criterion |
| --- | --- | --- |
| REQ-001 | A post needs text, at least one photo, or both. | The Post button is disabled while text is blank and no photo is attached. |
| REQ-002 | Post text is limited to 2,000 characters. | Text beyond 2,000 characters cannot be entered. |
| REQ-003 | A post has at most 4 photos. | Trying to add a fifth photo shows "You can add up to 4 photos." |
| REQ-004 | Photos are shrunk before upload. | An uploaded photo is no larger than 1600px on its longest side. |
| REQ-005 | A failed post keeps the draft. | If posting fails, the dialog stays open with the same text and photos. |
| REQ-006 | Pressing Post twice creates one post. | Double-tapping Post results in exactly one new post. |
| REQ-007 | Authors can edit their posts' text and photos. | After editing and saving, the post shows the new content and "Edited". |
| REQ-008 | Authors can delete their posts after confirming. | Confirming delete removes the post, its reactions, and its comments for everyone. |
| REQ-009 | Only the author and the admin can edit or delete. | Another member's post shows no more menu for a regular member. |

### FEAT-005 Reactions

| ID | Required behavior | Observable pass/fail criterion |
| --- | --- | --- |
| REQ-001 | Members react with Like or Haha. | Tapping Like makes it active and adds 1 to the Like count. |
| REQ-002 | One reaction per member per post. | Tapping Haha while Like is active switches to Haha; Like goes down by 1 and Haha goes up by 1. |
| REQ-003 | Tapping the active reaction removes it. | Tapping an active Like returns it to inactive and lowers the count by 1. |
| REQ-004 | Failed reactions revert. | If saving fails, the button returns to its previous state and an error toast appears. |
| REQ-005 | Members can see who reacted. | Tapping the reaction summary lists every reacting member under All, Like, and Haha. |

### FEAT-006 Comments

| ID | Required behavior | Observable pass/fail criterion |
| --- | --- | --- |
| REQ-001 | Members comment on a post's page. | Sending a comment shows it at the bottom of S-07 with the author's name and "Just now". |
| REQ-002 | Comments are flat and oldest first. | Comments appear in the order they were sent with no reply option. |
| REQ-003 | Comments are limited to 500 characters and cannot be blank. | Send is disabled for blank text and input stops at 500 characters. |
| REQ-004 | Authors can delete their own comments after confirming. | "Delete" appears only on your own comments (and on all comments for the admin). |
| REQ-005 | The feed shows each post's comment count. | A post with 4 comments shows "4 comments" on its card. |

### FEAT-007 Admin moderation

| ID | Required behavior | Observable pass/fail criterion |
| --- | --- | --- |
| REQ-001 | The admin can delete any post. | Signed in as Len, another member's post shows "Delete post (admin)". |
| REQ-002 | The admin can delete any comment. | Signed in as Len, every comment shows "Delete". |
| REQ-003 | The admin cannot edit other members' posts. | The admin's menu on another member's post has no "Edit post". |
| REQ-004 | Admin powers cannot be gained from the browser. | A regular member who edits page code in the browser still cannot delete another member's post. |

## Data

| Entity | Fields | Rules |
| --- | --- | --- |
| Member | id, email, display name, bio, photo, is admin, joined at | One admin (Len). Name 2 to 40 characters; bio up to 160. |
| Post | id, author, text, photos (ordered, up to 4), created at, edited at | Text up to 2,000 characters; needs text or a photo. |
| Reaction | post, member, type (like or haha), created at | At most one per member per post; removed with the post. |
| Comment | id, post, author, text, created at | Up to 500 characters; removed with the post. |
| Invite | code or link, email, used at | Single use; only needed if the custom invite-link option is chosen. |

## Quality constraints

- Feed first view loads in under 3 seconds on a typical phone over mobile data (target, not yet measured).
- Images are lazy-loaded below the fold and always have reserved space.
- The minimum rules in FEAT-007/REQ-004 apply even though heavy security work is out of scope: members change only their own content and only invited people sign in.
- The layout works from 375px to 1440px wide with no horizontal scroll.

## Decisions and assumptions

**Confirmed by Len in chat (2026-10-18):**

- Invite-only for friends; join through an invite link.
- One shared feed for all members.
- Posts with text and photos; authors edit and delete their posts.
- Reactions are Like and Haha only.
- Flat comments; authors delete their own; no reactions on comments.
- Basic profile with name, photo, bio, and posts.
- Len is the admin.
- Plain HTML, CSS, and JavaScript; hosting is decided later.
- Accepted recommendations: show who reacted, comment count only in the feed, composer as a pop-up, up to 4 photos per post, single centered column on desktop, playful and colorful look.

**Proposed in this document and not yet confirmed:**

- The name Chismisan, the tagline, and the tone examples.
- Editing a post can change its photos as well as its text.
- The color, type, and icon choices, including the Nunito and Fredoka web fonts.
- Text limits (2,000 post, 500 comment, 160 bio, 40 name) and 10 posts per load.
- Forgotten passwords are handled by messaging Len rather than a reset flow.
- Light theme only.

## Open questions and approval

1. **Backend:** Supabase is proposed but not approved; it is required before implementation, not before screen design.
2. **Invite mechanism:** an email sent from the backend dashboard or a shareable link built into the app; S-02 works for both.
3. **Removed members:** when Len removes a member, should their posts and comments stay or be deleted? Proposed: deleted.
4. **Password reset:** keep "Message Len", or add an email reset flow?

Approval: none recorded yet; this revision awaits Len's approval in chat.
