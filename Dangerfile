# Sometimes it's a README fix, or something like that - which isn't relevant for
# including in a project's CHANGELOG for example
declared_trivial = github.pr_title.include? "#trivial"

# Make it more obvious that a PR is a work in progress and shouldn't be merged yet
warn("PR is classed as Work in Progress") if github.pr_title.include? "[WIP]"

# Warn when there is a big PR
warn("Big PR") if git.lines_of_code > 500

can_merge = github.pr_json["mergeable"]
warn("This PR cannot be merged yet.", sticky: false) unless can_merge

has_source_changes = !git.modified_files.grep(/BitriseCocoaheads/).empty?
has_tests_changes = !git.modified_files.grep(/BitriseCocoaheadsTests/).empty?


if has_source_changes && !has_tests_changes
  warn("Update the library but not update the tests 🤔.", sticky: false)
end

# --------------------------------------------------------------------------------------------------------------------
# Run SwiftLint
# --------------------------------------------------------------------------------------------------------------------

swiftlint.lint_files inline_mode: true