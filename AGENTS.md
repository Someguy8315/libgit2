# Fork versioning and releases

- This fork tracks upstream libgit2 and adds gitstatus-specific patches. Preserve upstream's version in its version headers/CMake metadata; do not increment the upstream patch version for a fork-only fix or extension.
- Identify fork releases with the existing tag scheme: `1.9.7-gitstatus`, `1.9.7-gitstatus.1`, `1.9.7-gitstatus.2`, and so on. Increment the fork suffix once per tested dependency release, not once per implementation commit. For a new upstream base, use that base version and restart its fork suffix sequence after checking existing tags.
- A fork release may include fixes, optimizations, or new gitstatus-only APIs without pretending to be a new upstream libgit2 release. Document compatibility changes explicitly; the fork suffix is a release sequence, not a promise of API compatibility.
- Documentation/test-only changes need no new release tag unless explicitly included in a release. The gitstatus superproject's exact submodule commit is the authoritative dependency pin; tags provide named release checkpoints.

## Tags and publication

- Commit, tag creation, pushing, and release publication require their own requested scope. Do not automatically tag or push when asked only to fix code or bump a version.
- Before creating an annotated fork release tag, inspect local and remote tags, require a clean tree, and verify the affected library behavior and gitstatus integration on native Linux; Windows-specific code (`win32` sources) is kept but cannot be built or tested here, so state that when a change touches it. Follow gitstatus's release checks when this change is being shipped in the daemon. Do not label failed or incomplete verification as a tested release.
- Keep upstream tags unchanged. Never move or overwrite a published fork tag; corrections get a new suffix.
- When publication is requested, ensure the commit is reachable from an appropriate fork branch, including when developed on a detached submodule HEAD. Push that branch and any explicitly requested tag before publishing the gitstatus commit that pins it.
- Push named refs only, never all tags indiscriminately. Do not rewrite published history or force-push without explicit authorization.
- A fork tag does not itself require a daemon version bump. If the superproject adopts the dependency change for a daemon release, apply gitstatus's versioning rules there; the two version numbers need not move in lockstep.
