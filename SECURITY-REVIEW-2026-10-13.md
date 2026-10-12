# Security review — 2026-10-13

Prepared by i729. This review records tested source changes; it is not a certification of the deployed service.

## Change

Require configured secrets for webhook/panel operations, bind redemption disclosures to independently verified chat-to-UID mappings, protect visitor statistics with an external header key, and keep visitor storage outside the web root. Remove embedded administrator identity and pin deployment host keys and workflow actions.

## Validation

PHP syntax checks passed; seven empty-secret/wrong-key/ownership checks passed; workflow shell fragments passed bash syntax validation.

## Required before rollout

Set private WEBHOOK_SECRET/PANEL_AUTO_SYNC_SECRET, VISIT_ADMIN_KEY and VERIFIED_CHAT_UIDS after independent ownership verification. Do not derive trusted bindings from a customer-entered UID. Configure HOSTINGER_KNOWN_HOSTS and HOSTINGER_LOCK_DIR privately. Manually deploy protected PHP paths; the existing safe-deploy allowlist excludes them. Retire any old public analytics file and old exposed statistics key.

## Scope

Source and locally fetched Git branches/tags/available pull-request heads were inspected. Private production settings, actual database policies, deployed binaries, backup stores, and third-party service permissions were not changed. Current-source cleanup does not remove data from Git history, existing forks, cached copies, or previously downloaded assets. Sensitive values are intentionally omitted.
