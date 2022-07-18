# Feature Flags

Easily enable or disable features for experimentation or slow rollouts

- https://www.growthbook.io/)

https://software.rajivprab.com/2019/12/19/when-feature-flags-do-and-dont-make-sense/

### Simplest

Store in a db

name | is_active

Then write api to fetch is_active for that name before enabling. Or just fetch all feature flags on load and store in cookie or localStorage so persists. Hash user_id and name into % so stable percentage difference. Add custom flagging for user field and add in flags check.

#### Why feature flag provider?

A feature flag provider has a seperate db, audit log, user interface, code to automatically keep clientside flags updated(worker with socket), **enable for selective users**,

Providers:

- LaunchDarkly
- Posthog
- [Growthbook](