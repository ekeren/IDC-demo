![cloudbees feature management](https://1ko9923xosh2dsbjsxpwqp45-wpengine.netdna-ssl.com/wp-content/themes/rollout/images/rollout_white_logo1.png)

[![integration status](https://app.rollout.io/badges/62ab387e67e477c66f32e381)](https://app.rollout.io/app/62978f616063e0a2753d64d8/settings/info)

this repository is a yaml represnetation for rollout configuration, it is connected (see badge for status) to rollout service via [rollout's github app](https://github.com/apps/rollout-io)
configuration as code allows the entire configuration of rollout's state to be stored as source code. it integrates rollout's ui with engineering existing environment. this approach brings a lot of benefits.


# what is rollout
rollout is a multi-platform, infrastructure as code, software as a service feature management and s configuration solution.

# what are feature flags

feature flags is a powerfull technique based on remotetly and conditionaly opening/closing features threw the entire feature developement and delivery process.  as martin fowler writes on [feature toggles (aka feature flags)](https://martinfowler.com/articles/feature-toggles.html)

> feature toggles (often also refered to as feature flags) are a powerful technique, allowing teams to modify system behavior without changing code. they fall into various usage categories, and it's important to take that categorization into account when implementing and managing toggles. toggles introduce complexity. we can keep that complexity in check by using smart toggle implementation practices and appropriate tools to manage our toggle configuration, but we should also aim to constrain the number of toggles in our system.

you can read more about the advantages of having rollout configuration stored and treated as code in [rollout's support doc](https://support.rollout.io/docs/configuration-as-code)


# repository, directories and yaml structure
## branches are environments

every environment on rollout dashboard is mapped to a branch in git. the same name that is used for the environment will be used for the branch name. the only exception being production environment which is mapped to `master` branch

## directory structure

rollout repository integration creates the following directory structure:
```
.
├── experiments             # experiments definitions
│   └──  archived           # archived experiments definitions
├── target_groups           # target groups definitions
└── readme.md
```

- all experiments are located under the experiment folder
- all archived experiments are located under the `experiments/archived` folder

## experiment examples

### false for all users
```yaml
flag: default.followingview
type: experiment
name: following view
value: false
```
this yaml representation in rollout's dashboard:
![dashboard](https://files.readme.io/00b37e6-screen_shot_2018-12-03_at_11.47.56.png)
### 50% split
```yaml
flag: default.followingview
type: experiment
name: following view
value:
  - option: true
    percentage: 50
```
this yaml representation in rollout's dashboard:
![dashboard](https://files.readme.io/5af4d9e-screen_shot_2018-12-03_at_12.01.28.png)
### open feature for qa and beta users on version 3.0.1, otherwise close it
```yaml
flag: default.followingview
type: experiment
name: following view
conditions:
  - group:
      name:
        - qa
        - beta users
    version:
      operator: semver-gte
      semver: 3.0.1
    value: true
value: false
```
this yaml representation in rollout's dashboard:
![dashboard](https://files.readme.io/6884476-screen_shot_2018-12-03_at_12.04.13.png)
### open feature for all platform beside android
```yaml
flag: default.followingview
type: experiment
name: following view
platforms:
  - name: android
    value: false
value: true
```
dashboard default platfrom configuration:
![dashboard](https://files.readme.io/461c854-screen_shot_2018-12-04_at_10.19.59.png)
dashboard android configuration:
![dashboard](https://files.readme.io/1aafd04-screen_shot_2018-12-03_at_21.39.52.png)
## experiment yaml

this section describes the yaml scheme for an experiment. it is a composite of 3 schemas:


-  [root schema ](doc:configuration-as-code#section-root-schema)  - the base schema for experiment
-  [splited value schema](doc:configuration-as-code#section-splitedvalue-schema)  - represents a splited value -  a value that is distributed among different instances based on percentage
-  [scheduled value schema](doc:configuration-as-code#section-scheduledvalue-schema)  - represents a scheduled value -  a value that is based on the time that the flag was evaluated
-  [condition schema](doc:configuration-as-code#section-condition-schema)  - specify how to target a specific audience/device
-  [platform schema](doc:configuration-as-code#section-platform-schema)  - specify how to target a specific platform



### root schema
an experiment controls the flag value in runtime:

```yaml
# yaml api version
# optional: defaults to "1.0.0"
version: semver

# yaml type (required)
type: "experiment"

# the flag being controlled by this experiment (required)
flag: string

# the available values that this flag can be
# optional=[false, true]
availablevalues: [string|bool]

# the name of the experiment
# optional: default flag name
name: string

# the description of the experiment
# optional=""
description: string

# indicates if the experiment is active
# optional=true
enabled: boolean

# expriment lables
# optional=[]
labels: [string]|string

# stickiness property that controls percentage based tossing
# optional="rox.distict_id"
stickinessproperty: string

# platfrom explicit targeting
# optional=[]
platforms: [platfrom]  # see platfrom schema

# condition and values for default platfomr
# optional=[]
conditions: [condition] # see condition schema

# value when no condition is met
# optional
#  false for boolean flags
#  null for enum flags  (indicates default value)
value: string|boolean|[splitedvalue]|[scheduledvalue]|null
```

### splitedvalue schema
```yaml
# percentage, used for splitting traffic across different values
# optional=100
percentage: number

# the value to be delivered
option: string|boolean
```
### scheduledvalue schema
```yaml
# the date from which this value is relevant
# optional=undefined
from: date

# percentage, used for splitting traffic across different values
# optional=100
percentage: number
```
### condition schema

the condition is a pair of condition and value, an array of conditions can be viewed as an if-else statement by the order of conditions

the schema contains three types of condition statements
- dependency - express flag dependencies, by indicating flag name and expected value
- groups - a list of target-groups and the operator that indicates the relationship between them (`or`|`and`|`not`)
- version -  comparing the version of
[/block]
the relationship between these items is `and`, meaning:
       if the dependency is met `and` groups matches `and` version matches  `then` flage=value

here is the condition schema
```yaml
# condition this flag value with another flag value
dependency:
    # flag name
    flag: string
    # the expected flag value
    value: string|boolean

# condition flag value based on target group(s)
group:
    # the logical relationship between the groups
    # optional = or
    operator: or|and|not

    # name of target groups
    name: [string]|string

# condition flag value based release version
version:
    # the operator to compare version
    operator: semver-gt|semver-gte|semver-eq|semver-ne|semver-lt|semver-lte

    # the version to compare to
    semver: semver

# value when condition is met
value: string|boolean|[splitedvalue]|[scheduledvalue]|null
```
### platform schema
the platform object indicates a specific targeting for a specific platform

```yaml
# name of the platform, as defined in the sdk running
name: string

# override the flag name, when needed
# optional = experiment flag name
flag: string

# condition and values for default platfomr
# optional=[]
conditions: [condition] # see condition schema

# value when no condition is met
# optional
#  false for boolean flags
#  null for enum flags  (indicates default value)
value: string|boolean|[splitedvalue]|[scheduledvalue]|null # see value schema
```


## target group examples
### list of matching userid
```yaml
type: target-group
name: qa
conditions:
  - operator: in-array
    property: soundcloud_id
    operand:
      - 5c0588007cd291cca474454f
      - 5c0588027cd291cca4744550
      - 5c0588037cd291cca4744551
      - 5c0588047cd291cca4744552
      - 5c0588047cd291cca4744553
```

![dashboard](https://files.readme.io/7affbbe-screen_shot_2018-12-03_at_21.47.05.png)
### using number property for comparison

```yaml
type: target-group
name: dj
conditions:
  - operator: gte
    property: playlist_count
    operand: 100
description: users with a lot of playlists
```

on rollout dashboard
![dashboard](https://files.readme.io/dcb562f-screen_shot_2018-12-03_at_21.43.19.png)
## target group yaml

a target group is a set of rules on top of custom properties that are defined in runtime, it is used in experiments conditions

```yaml
# yaml api version
# optional: defaults to "1.0.0"
version: semver

# yaml type (required)
type: "target-group"

#target group name
name: string

# target group description
# optional = ""
description: string

# the logical relationship between conditions
# optional = and
operator: or|and

# array of conditions that have a logical and relationship between them
conditions:
    # the custom property to be conditioned (first operand)
  - property: string

    # the operator of the confition
    operator: is-undefined|is-true|is-false|eq|ne|gte|gt|lt|lte|regex|semver-gt|semver-eq|semver-gte|semver-gt|semver-lt|semver-lte

    # the second operand of the condition
    # optional - based on operator  (is-undefined, is-true, is-false)
    operand: string|number|[string]
```

# see also:
- using roxy docker image for microservices automated testing and local development [here](https://support.rollout.io/docs/microservices-automated-testing-and-local-development)
- configuration as code advantages [here](https://support.rollout.io/docs/configuration-as-code#section-advantages-of-configuration-as-code)
- integration walkthrough [here](https://support.rollout.io/docs/configuration-as-code#section-connecting-to-github-cloud)


please contact support@rollout.io for any issues questions or suggestions you might have
