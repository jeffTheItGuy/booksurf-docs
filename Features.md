# Features

---

## Semantic Search

Semantic search uses AI-generated vector embeddings to find public folders by meaning, not just exact keyword matches. Typing a concept like "productivity tools for developers" will surface relevant folders even if none of them use those exact words.

### How It Works

- **Embedding generation** — when you submit a query, it is converted into a numeric vector using an AI embedding model. Each public folder has a pre-computed embedding stored in the database.
- **Vector similarity** — the search ranks folders by cosine similarity between your query embedding and each folder's embedding. Folders whose meaning is closest to your query rank highest.
- **Similarity score** — each result carries a similarity score between 0 and 1. Scores closer to 1 indicate a stronger semantic match.
- **Text search fallback** — if the embedding search fails for any reason, the system automatically falls back to a keyword-based text search matching against folder names, descriptions, tags, and owner usernames. Fallback results are assigned a neutral similarity score of 0.5.

### Using Search

- **Search bar location** — the search bar is embedded in the top navigation bar on all tabs. Press Enter or click the Search button to execute.
- **Clear button** — an × button appears inside the search bar as soon as you start typing. Clicking it clears the input without leaving the search results view.
- **Back to Folders** — when search results are active, a back button replaces the normal tab row, letting you return to browsing without losing your place.
- **Phrase queries** — longer, descriptive queries tend to produce better results than single words. For example, "machine learning tutorials for beginners" is more effective than just "ML".

### Search Results

- **Infinite scroll** — results load 20 folders at a time. As you scroll to the bottom, more are fetched automatically.
- **Sort options** — results can be re-sorted by Relevance (default), Newest, or Most Popular.
- **Deduplication** — the same folder will never appear twice in a results list.
- **Empty state** — if no folders match your query, a clear message is shown with a button to reset the search.
- **Rate limits** — unauthenticated users can perform up to 40 searches per minute and 300 per hour. Logged-in users have higher limits of 60 per minute and 500 per hour.

### Search Tips

- Use natural language — write as if describing what you are looking for to a person, not a search engine.
- Try different phrasings if your first query returns few results.
- Search by concept rather than specific product names, e.g. "frontend design resources" instead of "Figma".
- Logging in unlocks higher rate limits and personalised result data such as your own vote status on each folder.

---

## Navigation & Browsing

The navigation bar sits at the top of every page and is the primary way to browse public folders. It combines tab-based browsing, tag filtering, and the search bar into a single compact header.

### Tabs

- **Trending** — available to everyone. Shows public folders ranked by views received in the last 24 hours, with recently published folders as a tiebreaker.
- **Featured** — available to everyone. Shows folders ranked by their featured score, a manually curated metric used by moderators to highlight high-quality collections.
- **For You** — only visible when logged in. Shows personalised folder recommendations based on your activity such as folders you follow, upvote, or bookmark.
- **My Folders** — only visible when logged in. Switches the tag row to show folder type filters instead of topic tags.

### Tag Filtering

- **Topic tags** — a scrollable row of topic tags: All, Tech, Education, Finance, Utils, Work, Lifestyle, Entertainment, News, Sports, and Social. Clicking a tag filters the current tab to only show folders with that tag.
- **Arrow navigation** — if there are more tags than fit on screen, left and right chevron buttons appear at the edges of the tag row.
- **My Folders tag row** — when My Folders is active, the tag row switches to three folder type filters: Private Folders, Public Folders, and Followed Folders.

### My Folders Types

- **Private Folders** — folders you have created that have not been made public. Only you can see these.
- **Public Folders** — folders you own that have been approved and published. Visible to all users.
- **Followed Folders** — public folders created by other users that you have followed.

### Responsive Layout

- **Wide screens** — tabs appear on the left side of the header and the search bar appears on the right.
- **Narrow screens (below 800px)** — the search bar moves above the tabs and both stack vertically.
- **Tag row** — always renders on its own row below the header on all screen sizes.

---

## Bookmark Manager

The Bookmark Manager is your private workspace for creating, organising, and managing folders and bookmarks before optionally sharing them publicly. All changes are staged locally and only committed to the server when you click **Save**.

### Folders

- **Create a folder** — click *Create New Folder* at the bottom of the list. You must provide a name (max 100 characters), an optional description (max 300 characters), and select a tag. The tag is required.
- **Edit a folder** — double-click the folder row or click the pencil icon on hover.
- **Delete a folder** — click the trash icon on hover. The folder and all its bookmarks are removed. This cannot be undone after you Save, but you can Undo before saving.
- **Limits** — Basic users can hold 3 private folders; Members can hold 5.
- **Folder tags** — each folder must be tagged (e.g. tech, education, finance).

### Bookmarks

- **Add a bookmark** — expand a folder and click *Add Bookmark*. Enter a title (max 100 characters) and a URL (max 2048 characters).
- **URL handling** — URLs are validated as you type. If you enter a URL without a protocol (e.g. `example.com`), `https://` is added automatically on save. HTTP URLs are auto-upgraded to HTTPS. Common typos are detected and suggested corrections are shown.
- **Edit a bookmark** — double-click the bookmark row or click the pencil icon on hover.
- **Delete a bookmark** — click the trash icon on hover.
- **Limits** — Basic users can store 15 bookmarks per folder; Members can store 20. You cannot save a new folder that has fewer than 3 bookmarks.

### Reordering

- **Drag and drop folders** — grab a folder row and drop it onto another folder to swap their positions.
- **Drag and drop bookmarks** — grab a bookmark and drop it onto another bookmark within the same folder to reorder, or drop it onto a different folder header to move it there.
- **Up / Down arrows** — each folder and bookmark row shows chevron arrows on hover for precise one-step reordering.

### Toolbar

Click the wrench icon in the action bar to toggle the toolbar. It provides batch operations and utility actions.

- **Select Folders** — enters folder selection mode. Click folders to select them, then use Delete to remove them all at once.
- **Select Bookmarks** — enters bookmark selection mode. Click bookmarks across any folder to select them. You can then **Move**, **Copy**, or **Delete** them in bulk.
- **Export** — downloads all your folders and bookmarks as a `bookmarks.json` file. Useful as a backup or for loading into the browser extension.
- **Import** — upload a previously exported JSON file. Imported folders are added alongside your existing ones.
- **Collapse All / Expand All** — toggle the expanded state of every folder at once.

### Undo, Redo & Save

- **Undo / Redo** — every action is recorded in a history stack. Use the Undo and Redo buttons to step through your changes freely before committing.
- **Save** — the Save button shows the number of pending changes. Clicking it sends a single batch request that applies all creates, edits, deletes, reorders, and moves at once.
- **Refresh** — reloads your folders from the server, discarding any unsaved local changes.
- **New folder minimum** — any newly created folder must contain at least 3 bookmarks before you can Save.

### Search

- **Real-time filtering** — type in the search bar to instantly filter folders and bookmarks. The search matches against folder names, descriptions, bookmark titles, bookmark URLs, and bookmark descriptions.
- Folders that do not match and contain no matching bookmarks are hidden from the list.
- Clear the search bar to return to the full view.

---

## Public Folders

Public folders are curated bookmark collections that you share with the entire Booksurf community. Once approved by moderators, your folder appears in the Trending and Featured feeds and is discoverable via semantic search.

### Requesting Public Status

- **Email verification required** — you must verify your email address before you can submit a public request.
- **Monthly request limit** — each account may submit 3 public folder requests per calendar month. The counter resets on the 1st of every month. Members get 5 requests reset immediately upon payment.
- **How to request** — hover over a private folder card and click the globe icon in the top-right corner. This opens the Request Public Status modal. Click Submit Request to send the folder for moderation review.
- **Minimum bookmarks** — a folder must contain at least 3 bookmarks.
- **Folder content rules** — folders must comply with the [Content Policy](content-policy.md).

### Moderation Process

- **Pending review** — after submitting, your folder enters a pending state. A clock icon appears on the folder card in your My Folders view.
- **Review time** — moderation typically takes 1–3 business days.
- **Approved** — the folder becomes publicly visible in all feeds and is indexed for semantic search. The clock icon is replaced by a globe icon.
- **Rejected** — the folder remains private. You may edit the folder and submit a new request (subject to your monthly limit).
- **No edits while pending** — the edit and delete controls on a folder card are hidden while the folder is awaiting review.

### Public Folder Card

- **View** — clicking the external link icon opens the full folder detail page.
- **Share** — the share icon opens a modal with a copyable link and one-click sharing to Twitter, Facebook, LinkedIn, and Reddit.
- **Follow** — logged-in users who do not own the folder can click the bookmark icon to follow it. You can follow a maximum of 10 folders.
- **Vote** — upvote or downvote a public folder using the arrow buttons. Clicking the same vote a second time removes it.
- **Report** — the flag icon lets logged-in non-owners submit a report. Categories include Spam, Inappropriate Content, Malicious Links, Copyright Violation, and Other.
- **View count** — the eye icon shows total impressions. Hovering reveals a breakdown of total views, unique users, and anonymous views.
- **Click count** — the cursor icon shows total bookmark clicks within the folder.
- **Author** — the owner's username is shown below the stats. Clicking it filters the feed to show all public folders by that user. Members display a blue verified badge; basic users display a grey badge.

### Following Folders

- Click the bookmark icon on any public folder card you do not own to follow it.
- Followed folders appear in the **Followed Folders** sub-tab under My Folders.
- You can follow a maximum of 10 folders. To follow a new one you must first unfollow an existing one.

### Stats & Analytics

- **Impressions** — recorded automatically when a public folder card enters the viewport and remains visible for at least 200 ms.
- **Bookmark clicks** — recorded each time a visitor clicks a bookmark link inside a public folder.
- **Trending algorithm** — the Trending tab orders folders by impressions received in the last 24 hours.
- **Featured score** — the Featured tab orders folders by a curated score assigned by the moderation team.

### Making a Folder Private

- **How to revert** — on your own public folder card, hover to reveal the lock icon and click it to open the Make Private modal.
- **What happens** — a full copy of the folder and all its bookmarks is created in your private folders. The public version is hidden from search immediately and scheduled for permanent deletion after 30 days.
- **Irreversible** — this action cannot be undone. The public listing will not be restored.
- **Email verification required** — your email must be verified before you can make a folder private.

---

## Membership

Join the Booksurf community and unlock additional benefits by donating any amount above $3.

- **Free Account** — access to all core features at no cost
- **Community Access** — share and discover resources with other members
- **Cloud Sync** — keep your bookmarks synced across all your devices
- **Personalized Experience** — get tailored recommendations based on your interests

**Member Benefits vs Basic:**

| Feature | Basic | Member |
|---|---|---|
| Private folders | 3 | 5 |
| Bookmarks per folder | 15 | 20 |
| Public requests/month | 3 | Reset to 5 on payment |
| Moderation priority | Standard | Priority |
| Feed ranking | Standard | Boosted |

> **Note:** Paying again before membership expires resets the membership, it doesn't extend it.