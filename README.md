[![Build Status](https://travis-ci.org/rosette-api/R.svg?branch=master)](https://travis-ci.org/rosette-api/nodejs)

# rosette-api

This is the Rosette API client binding for R.

## Getting Started
Install the module with: `install.packages('rosetteAPI')`, which will pull the release from CRAN

OR (recommended), since CRAN is potentially behind the latest release, due to the hurdles one must traverse in order to publish, install from GitHub using ```install_github("rosette-api/r-binding")```

Command line example:

```
$ R -e 'install.packages("devtools")
$ cat > installrosette.R << EOF
> library(devtools)
> install_github("rosette-api/r-binding")
> q()
> EOF
$ R --no-save < installrosettte.R
```

## Example using the Rosette API language detection endpoint
```R
library(rosetteApi)
library(jsonlite)

parameters <- list()
parameters[[ "contentUri" ]] <- "http://www.onlocationvacations.com/2015/03/05/the-new-ghostbusters-movie-begins-filming-in-boston-in-june/"

result <- api("0123456789", "categories", parameters)
# result is a list containing content and headers in native R.  Use jsonlite::toJSON to convert to JSON format.
print(jsonlite::toJSON(result$content, pretty = TRUE)
```
## API Parameters
| Parameter                     | Endpoint                                            | Required
| -------------                 |-------------                                        |------------- 
| content                    | categories, entities, language, morphology, relationships, sentences, sentiment, tokens, syntax_dependencies            | Either content or contentUri required |
| contentUri                      | categories, entities, language, morphology, relationships, sentences, sentiment, tokens, syntax_dependencies       | Either content or contentUri required |
| language                          | categories, entities, language, morphology, relationships, sentences, sentiment, tokens, name similarity                    | No |
| documentFile                      | categories, entities, language, morphology, relationships, sentences, sentiment, tokens                  | No |
| name1                 | name similarity               | Yes |
| name2               | name similarity| Yes |
| name    | name translation     | Yes |
| targetLanguage           | name translation           | Yes |
| entityType                 | name translation         | No |
| sourceLanguageOfOrigin        | name translation | No |
| sourceLanguageOfUse                         | name translation       | No |
| sourceScript                     | name translation               | No |
| targetScript                     | name translation                    | No |
| targetScheme                        | name translation          | No |
| options              | relationships        | No |
| accuracyMode              | relationships        | Yes |
| explain              | sentiment        | No |
| morphology             | morphology        | Yes |

## Docker ##
A Docker image for running the examples against the compiled source library is available on Docker Hub.

Command: `docker run -e API_KEY=api-key -v "<binding root directory>:/source" rosetteapi/docker-r`

Additional environment settings:
`-e ALT_URL=<alternative URL>`
`-e FILENAME=<single filename>`

## Additional Information
See [Rosette API site](https://developer.rosette.com/)
