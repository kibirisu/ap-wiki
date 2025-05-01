[Activity Vocabulary](https://www.w3.org/TR/activitystreams-vocabulary/)

[ActivityStreams](https://www.w3.org/TR/activitystreams-core/)

Data flow in activity pub is using json-ld format. The format allow linking additional data.

[HTTP Signatures](https://datatracker.ietf.org/doc/html/draft-ietf-httpbis-message-signatures)

[WebFinger](https://www.rfc-editor.org/rfc/rfc7033)
- Needed for compliance with Mastodon.
- Resolves user handles into urls.

[Server to Server Interactions](https://www.w3.org/TR/activitypub/#server-to-server-interactions)

> Servers communicate with other servers and propagate information across the social graph by posting activities to actors' inbox endpoints.

- Intro
    - Allows posting activities to actors' inbox.
    - Requires id (unless transient)
    - Enforce usage of `application/activity+json` header (json-ld???)
    - Recipients are determined by links between objects
        > In order to propagate updates throughout the social graph, Activities are sent to the appropriate recipients.
        > First, these recipients are determined through following the appropriate links between objects until you reach an actor,
        > and then the Activity is inserted into the actor's inbox (delivery).

- Delivery:
    - happens when:
        - an Activity being created in an actor's outbox with their Followers Collection as the recipient.
        - an Activity being created in an actor's outbox with directly addressed recipients.
        - an Activity being created in an actors' outbox with user-curated collections as recipients.
        - an Activity being created in an actor's outbox or inbox which references another object.
    - Requires properties:
        - `object` (e.g. `Create, Update, Delete, Follow, Add, Remove, Like, Block, Undo`)
        - `target` (`Add`, `Remove`)
    - Flow
        - looking up the targets' inboxes
        - posting to those inboxes
    - uses [`ActivityStreams` audience targeting](https://www.w3.org/TR/activitystreams-vocabulary/#audienceTargeting) to find out targets
