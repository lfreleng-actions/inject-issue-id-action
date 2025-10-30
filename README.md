<!--
SPDX-License-Identifier: Apache-2.0
SPDX-FileCopyrightText: 2025 The Linux Foundation
-->

# 🎟️ Add issue tracker to commit message body

Action to add an issue tracker reference to the body of a commit message.

## inject-issue-id-action

## Usage Example

Pass a JSON key/value lookup table to the action, either directly as a string,
or by passing in the contents of a variable (set either at the repository or
organisation level).

```yaml
- name: "Check/Add commit message issue tracker reference"
  uses: lfit/releng-reusable-workflows/.github/actions/inject-issue-id-action@main
  with:
      issue_id_lookup_json: ${{ vars.ISSUE_ID_LOOKUP_JSON }}
```

In the example above, the repository passes in the JSON data contained in
a variable configured called ISSUE_ID_LOOKUP_JSON.

Set/define this for the repository under:

GitHub Repository -> Settings -> Secrets and variables -> Actions -> Variables

## Inputs

issue_id_lookup_json is mandatory; issue_string and inject are optional
with default values.

<!-- markdownlint-disable MD013 -->

| Variable Name        | Required | Default     | Description                           |
| -------------------- | -------- | ----------- | ------------------------------------- |
| issue_id_lookup_json | True     | N/A         | JSON object of key/value pairs        |
| issue_string         | False    | "Issue-ID:" | Fixed preamble/string to embed/inject |
| inject               | False    | True        | When set false, checks for presence   |

<!-- markdownlint-enable MD013 -->

## Outputs

| Variable Name | Description                                   |
| ------------- | --------------------------------------------- |
| present       | Set true when ticket string found or injected |

## Limitations

This action uses `${{ github.actor }}` as the key to lookup, but also
reports the `${{ github.actor_id }}`, which is a GitHub facsimile to
the UNIX concept of a UID value.

## Future Enhancements

It may be desirable to use other GitHub parameters as keys in the JSON
value/lookup.
