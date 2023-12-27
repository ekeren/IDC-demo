

<h1>CloudBees Feature Management</h1>

<p>
<a href="https://app.rollout.io/badges/62ab387e67e477c66f32e381" target="_blank">
<img src="https://1ko9923xosh2dsbjsxpwqp45-wpengine.netdna-ssl.com/wp-content/themes/rollout/images/rollout_white_logo1.png" alt="Rollout Status">
</a>
</p>

<h2>What is Rollout?</h2>

<p>
Rollout is a multi-Platform infrastructure as code, software as a service feature management and remote Configuration solution.
</p>

<h2>What Are Feature Flags?</h2>

<p>
Feature Flags is a powerful technique based on remotely and conditionally opening/closing features through the entire feature development and delivery process. As Martin Fowler writes on <a href="https://martinfowler.com/articles/feature-toggles.html" target="_blank">Feature Toggles (aka Feature Flags)</a>, feature toggles introduce complexity, but they can be managed with smart toggle implementation practices and appropriate tools.
</p>

<h2>Repository, Directories, and YAML Structure</h2>

<p>
Every environment on Rollout dashboard is mapped to a branch in git, and the same name is used for the environment and the branch name, except for the production environment, which is mapped to the <code>master</code> branch. The following directory structure is created:
</p>

<ul>
<li><code>experiments</code>: Contains all experiments definitions</li>
<li><code>target_groups</code>: Contains all target groups definitions</li>
</ul>

<h2>Experiment Examples</h2>

<p>
Here are some examples of experiments:
</p>

<ul>
<li><code>flag: default.followingView</code>: Experiment to turn off the following view feature for all users</li>
<li><code>flag: default.followingView</code>: Experiment to turn off the following view feature for all users</li>
<li><code>flag: default.followingView</code>: Experiment to turn off the following view feature for all users</li>
</ul>

<h2>Target Group Examples</h2>

<p>
Here are some examples of target groups:
</p>

<ul>
<li><code>type: target-group</code>: List of matching user IDs</li>
<li><code>type: target-group</code>: Using number property for comparison</li>
</ul>

<h2>Target Group YAML</h2>

<p>
A target group is a set of rules on top of custom properties that are defined in runtime, it is used in experiments conditions. Here is the YAML schema for a target group:</p>

<code>
# Yaml api version
# Optional: defaults to "1.0.0"
version: Semver

# Yaml Type (required)
type: "target-group"

# Target Group Name
name: String

# Target Group description
# Optional = ""
description: String

# The logical relationship between conditions
# Optional = and
operator: or|and

