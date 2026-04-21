# blog-comment

Backing store for comments on [foooling.com](https://foooling.com),
powered by [giscus](https://giscus.app) on top of GitHub Discussions.

Each article page on the blog mounts the giscus widget with
`data-mapping="pathname"`, so a new Discussion is auto-created the first
time someone comments on `/post/{id}/`.

## Configuration in use

- Repo: `fooling/blog-comment` (public)
- Discussion category: **Announcements** (Announcement type — only
  maintainers can create new threads, giscus creates them on demand)
- Mapping: `pathname`
- Strict title matching: on
- Theme: `dark_dimmed`
- Lang: `zh-CN`

## Moderating

- To lock a thread: open the Discussion → Lock conversation.
- To delete a comment: open the Discussion → delete the comment.
- To hide a spammy user: report via the Discussion UI.

## Backup

Comments live in GitHub Discussions. Export with:

```bash
gh api graphql -f query='
  query($owner: String!, $repo: String!) {
    repository(owner: $owner, name: $repo) {
      discussions(first: 100) {
        nodes { title url body comments(first: 100) { nodes { body author { login } } } }
      }
    }
  }' -F owner=fooling -F repo=blog-comment
```
