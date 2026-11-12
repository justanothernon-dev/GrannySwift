# Swift-first glue around upstream engines

The earlier AppleSuite glue was Python; GrannySwift replaces that routing and adaptation with project-owned Swift, but keeps a capable upstream engine in its own language (osxphotos for Photos, for example) instead of rewriting every provider. We accept some non-Swift dependencies rather than duplicate engines that already do the job.
