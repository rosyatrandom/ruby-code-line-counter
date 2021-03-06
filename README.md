# ruby-code-line-counter
VERSION 0.3
_________________

## Description:

CLC is a Ruby utility that can analyse Ruby files, from a given list of paths,
and return a count of:
- lines with comments
- blank lines
- lines with code
- any/all of the above

Any directory paths supplied to CLC will be scanned for any Ruby files within.

CLC can return:
- counts for each file analysed
- a summary count for all files analysed
- both of the above

CLC will also report any invalid paths returned to it.

Return format is a hash, full format as follows:
```
{
  (file_name_1) => { code: (count), blank: (count), comment: (count) },
  ...
  summary: { code: (count), blank: (count), comment: (count) },
  invalid_paths: [(path_1), ...]
}
```
Only counts and outputs that have been selected will appear in the hash.

## Usage:

CLC can be run from the command line, or from within another Ruby program/environment.

If run from the command line without arguments, help text will be displayed.

If run from within Ruby, options can be set with:
- `#set_paths` (paths can also be set from `::new`)
- `#set_counts`
- `#set_outputs`

Options that can be used are available as constants within CLC

## Implementation Details:

CLC works by using Ripper to tokenize Ruby code and determine what tokens are present on
which lines. This may seem like overkill, but it would be impossible to detect where comments
begin and end, and whether they are actually comments, without building a complicated state 
machine to effectively do the same job.

## Notes:

CLC currently only has partial test coverage.

CLC will raise an error if passed invalid arguments from the command line.

CLC has only been tested on Ruby 2.6.0.

## Version History:

### 0.1
- Initial implementation

### 0.2
- Some minor internal naming / style changes
- Fixed bug: lines within some multi-line strings would not be
  counted due to being counted as single token.

### 0.3
- Fixed bug: individual files not processable
- refactoring to decouple code elements

## To-Do:

- Re-work as a proper Gem
- Complete testing
- Ensure compatibiliuty with earlier versions of Ruby
- Handle error raised on incorrect CLI switches

