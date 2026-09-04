# Contributing Guidelines

## Reporting Issues

Before creating a new Issue, please check first if a similar Issue [already exists](https://github.com/oceanbase-driver/go-oceanbase-driver/issues?state=open) or was [recently closed](https://github.com/oceanbase-driver/go-oceanbase-driver/issues?direction=desc&page=1&sort=updated&state=closed).
When reporting connection problems against OceanBase, include the server
version (`SELECT BANNER FROM V$VERSION`) and whether the tenant is MySQL
or Oracle mode. Upstream driver issues belong to
[go-sql-driver/mysql](https://github.com/go-sql-driver/mysql/issues).

## Contributing Code

By contributing to this project, you share your code under the Mozilla Public License 2, as specified in the LICENSE file.

### Code Review

Everyone is invited to review and comment on pull requests.
If it looks fine to you, comment with "LGTM" (Looks good to me).

If changes are required, notice the reviewers with "PTAL" (Please take another look) after committing the fixes.
