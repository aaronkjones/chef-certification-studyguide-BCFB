# BASIC CHEF FLUENCY BADGE
This study guide is for the [Basic Chef Fluency Badge](https://training.chef.io/basic-chef-fluency-badge).  
Feel free to contribute by submitting a GitHub Pull Request.  

# CHEF BASIC TERMINOLOGY
## RESOURCES
* Idempotency/convergence - test & repair model 
	* *idempotence* - same command produces the same result no matter how many times it is run
		* (e.g. mkdir -p /tmp/files)
	* *convergence* - changes are only made if they need to be
* Common resources and their actions
	* [Resource Reference](https://docs.chef.io/resource_reference.html)
* Default actions
	* [Resource Reference](https://docs.chef.io/resource_reference.html)
* The ':nothing' action
	* Use `nothing` to prevent the task execution. Use subscribe with this to only act when other resource completes. 
* The 'supports' directive
	* [metadata.rb](https://docs.chef.io/config_rb_metadata.html)
```
supports
    Show that a cookbook has a supported platform. Use a version constraint to define dependencies for platform versions: < (less than), <= (less than or equal to), = (equal to), >= (greater than or equal to), ~> (approximately greater than), or > (greater than). To specify more than one platform, use more than one supports field, once for each platform.

    For example, to support every version of Ubuntu:

    supports 'ubuntu'

    or, to support versions of Ubuntu greater than or equal to 12.04:

    supports 'ubuntu', '>= 12.04'

    or, to support only Ubuntu 14.10:

    supports 'ubuntu', '= 14.10'

    Here is a list of all of the supported specific operating systems:

        %w( aix amazon centos fedora freebsd debian oracle mac_os_x redhat suse opensuse opensuseleap ubuntu windows zlinux ).each do |os|
          supports os
        end				
```
* The 'not_if' and 'only_if' directives
  * [Common Functionality](https://docs.chef.io/resource_common.html#attributes)
  * `not_if` Prevent a resource from executing when the condition returns true.
  * `only_if` Allow a resource to execute only if the condition returns true. 
* Resource extensibility
  * [Custom Resources](https://docs.chef.io/custom_resources.html)

## RECIPES
* What a recipe is
  * [About Recipes](https://docs.chef.io/recipes.html)
* Importance of the resource order 
  * [About Run-lists](https://docs.chef.io/run_lists.html#)
* How to use 'include_recipe'
  * [Include Recipe](https://docs.chef.io/dsl_recipe.html#include-recipes)
* What happens if a recipe is included multiple times in a run_list 
```
If a specific recipe is included more than once with the include_recipe method or elsewhere in the run_list directly, only the first instance is processed and subsequent inclusions are ignored.
```
* The 'notifies' and 'subscribes' directives
  * [Notifies](https://docs.chef.io/resource_common.html#notifies)
  * [Subscribes](https://docs.chef.io/resource_common.html#subscribes)

## COOKBOOKS
* Cookbook contents
  * [Cookbook Components](https://docs.chef.io/cookbooks.html)
* Naming conventions
  * [Cookbook Naming](https://docs.chef.io/ruby.html#cookbook-naming)
* Cookbook dependencies
  * [Cookbook Directories and Metadata](https://docs.chef.io/cookbook_repo.html#settings)
  * [metadata.rb](https://docs.chef.io/config_rb_metadata.html)
  * [Berkshelf](https://docs.chef.io/berkshelf.html)
* The default recipe
  * The default recipe does not need to be specified. For example if you wanted to include apache2::default in your wrapper cookbook, you can simply write `include_recipe 'apache2'` instead of `include_recipe 'apache2::default'`.

## CHEF SERVER  
* How the Chef server acts as an artifact repository
  * [Chef Server Components](https://docs.chef.io/server_components.html)
* How the Chef server acts as an index of node data
  * [Chef Server Components](https://docs.chef.io/server_components.html)
* Chef solo vs Chef server
  * [Chef Solo](https://docs.chef.io/chef_solo.html)
  * `chef-solo` is a command that executes chef-client in a way that does not require the Chef server in order to converge cookbooks.
* Chef server's distributed architecture
  * [Server Compontents](https://docs.chef.io/server_components.html#server-components)
* Scalability
  * [Scaling the Chef Server](https://docs.chef.io/server_components.html#scaling-the-chef-server)

## SEARCH
* What search is
  * [About Search](https://docs.chef.io/chef_search.html)  
  * `Search` indexes allow queries to be made for any type of data that is indexed by the Chef server, including:
    - data bags (and data bag items)
    - environments
    - nodes 
    - roles

* How to search for node information
  * https://github.com/aaronkjones/chef-knife-search-cheatsheet
* What and how many search indexes Chef server maintains 
* What a databag is
> A data bag is a global variable that is stored as JSON data and is accessible from a Chef server. A data bag is indexed for searching and can be loaded by a recipe or accessed during a search.
* How to use search for dynamic orchestration 
* How to invoke a search from the command line
	* knife search
## CHEF CLIENT
* What the Chef client is
	* [Chef Client Overview](https://docs.chef.io/chef_client_overview.html)
	> A chef-client is an agent that runs locally on every node that is under management by Chef.
* The function of Chef client vs the function of Chef server 
	* [Chef Client Overview](https://docs.chef.io/chef_client_overview.html)
* What 'why-run' is
	* [About why-run Mode](https://docs.chef.io/chef_client_overview.html#about-why-run-mode)
    > Like a "dry-run", why-run mode is a way to see what the chef-client would have configured, had an actual chef-client run occurred
* How to use '--local-mode'
    * [Run in Local Mode](https://docs.chef.io/ctl_chef_client.html#sts=Run%20in%20Local%20Mode%C2%B6)
    > Local mode is a way to run the chef-client against the chef-repo on a local machine as if it were running against the Chef server
* How the Chef client and the Chef server communicate The Chef client configuration


## NODES
* What a node is
  * [About Nodes](https://docs.chef.io/nodes.html)
  * > A node is any machine—physical, virtual, cloud, network device, etc.—that is under management by Chef
* What a node object is
  * [Node Objects](https://docs.chef.io/nodes.html#node-objects)
  * > The node object consists of the run-list and node attributes, which is a JSON file that is stored on the Chef server. The chef-client gets a copy of the node object from the Chef server during each chef-client run and places an updated copy on the Chef server at the end of each chef-client run.
* How a node object is stored on Chef server 
  * > At the end of every chef-client run, the node object that defines the current state of the node is uploaded to the Chef server so that it can be indexed for search.
* How to manage nodes
  * [Manage Nodes](https://docs.chef.io/nodes.html#manage-nodes)
* How to query nodes 
  * `knife node list`
* How to name nodes
  * When bootstrapping: 
    * `-N NAME, --node-name NAME`
  * When editing
    * `knife node edit`, change the name
    

## RUN LIST
* What a run_list is
  * [About Run-lists](https://docs.chef.io/run_lists.html)
  * > An ordered list of roles and/or recipes that are run in the exact order defined in the run-list 
* What nested run_lists are
  * > Roles contain a run list. Roles included in the run_list of other roles are nested within.
* Where a run_list is stored
  * > Stored as part of the node object on the Chef server
* What does a run_list consist of 
  * Empty or Roles and Recipes
* How to look up run_lists
  * `knife node show -r`
* How to set and change run_lists
  * `knife node run_list set NODE_NAME RUN_LIST_ITEM`
  * `knife node run_list add NODE_NAME RUN_LIST_ITEM`
  * `knife node run_list remove NODE_NAME RUN_LIST_ITEM`
## ROLES
* What roles are
  * [About Roles](https://docs.chef.io/roles.html)
  * > A role is a way to define certain patterns and processes that exist across nodes in an organization as belonging to a single job function.

* How a role ensures code consistency across nodes 
* Where roles can be stored
  * > Role data is stored in two formats: as a Ruby file that contains domain-specific language and as JSON data
* How roles are defined
  * `"role[name]"`
  * Inside JSON file: `"chef_type": "role",`
* What the components of a role are
  * [About Roles](https://docs.chef.io/roles.html)
* Roles vs recipes vs run_lists
* How to name roles
* How to apply roles to nodes
* How to edit roles

## ENVIRONMENTS
* The purpose of environments
  * [About Environments](https://docs.chef.io/environments.html)
  > An environment is a way to map an organization’s real-life workflow to what can be configured and managed when using Chef server. Every organization begins with a single environment called the _default environment, which cannot be modified (or deleted).
* How to use environments to manage cookbook release cycles 
  * By pinning cookbooks in environments. For example, given 3 enviornments: dev, staging, and prod; a cookbook called Base could be pinned as such
    * dev: 2.0.0
    * staging: 2.0.0
    * prod: 1.9.2
  * [knife environment](https://docs.chef.io/knife_environment.html)
* How to use environments to constrain cookbooks
* Using `cookbook_versions`. See [Ruby DSL](https://docs.chef.io/environments.html#ruby-dsl)
* How to put nodes into an environment
  * [Move Nodes](https://docs.chef.io/environments.html#move-nodes)

## INFRASTRUCTURE AS CODE
* What the advantages are of defining infrastructure as code 
  * Cost
  * Speed
  * Risk reduction
* The reasons for defining infrastructure as code
  * Automation, reduction of manual steps to focus efforts on tasks that add value
  * Error reduction, with automation less errors likely to occur
  * Speed, faster to execute one or two commands vs manually creating
  * Version control, changes are visible in version control 
  * Validation before deployment, test new changes before pushing them to deployment environment
* The difference between rolling back and rolling forward
  * Rolling back: applying a previous version
  * Rolling forward: reapplying the current version

## DESIRED STATE CONFIGURATION
* The imperative vs the declarative approach to configuration management 
  * Declarative (functional): What thing should be done. Example: `nginx should be installed`
  * Imperative (procedural): How a thing should be done. Example: `apt-get install nginx`
* The push vs the pull approach
  * Push: You push the configuration to the server to be changed
  * Pull: The server to be changed pulls the configuration from a source
* What Windows DSC is
  * [dsc_resource](https://docs.chef.io/resource_dsc_resource.html)
  * > Desired State Configuration (DSC) is a feature of Windows PowerShell that provides a set of language extensions, cmdlets, and resources that can be used to declaratively configure software
* What happens if you remove a resource from a recipe
  * The resource does not run, no change is made to the target system

## SUPERMARKET
* The Supermarket value proposition
* What you can store in Supermarket
  * Cookbooks
* What a private Supermarket is
  * On-prem hosted
* When to use a private Supermarket
  * A private Chef Supermarket may be installed on-premise behind the firewall on the internal network.
  * Cookbook retrieval from a private Chef Supermarket is often faster than from the public Chef Supermarket because of closer proximity and fewer cookbooks to resolve. 
  * A private Chef Supermarket can also help formalize internal cookbook release management processes (e.g. “a cookbook is not released until it’s published on the private Chef Supermarket”).
* If Supermarket is a free or a premium feature
  * Free
* If the items in Supermarket are free or cost money
  * Free

## CHEF DK
* The Chef DK value proposition
* Specific features of test-driven development (TDD) 
  * reduction in defect rates
* Tools packaged in Chef DK
  * Foodcritic
  * Kitchen
  * ChefSpec
  * InSpec

## TEST KITCHEN
* The Test Kitchen value proposition
* What TDD is
  * Test Driven Development is a development technique where you must first write a test that fails before you write new functional code
  * Regarding Chef, to exercize TDD, one could write unit tests with [ChefSpec](https://docs.chef.io/chefspec.html) and integration tests with [InSpec](https://www.inspec.io) prior to writing recipe code. 
  * ChefSpec [examples](https://github.com/chefspec/chefspec/tree/master/examples)
  * InSpec [examples](https://github.com/chef/inspec/tree/master/examples)
* The platforms supported by Test Kitchen
  * kitchen-vagrant: Ubuntu, CentOS, Debian, FreeBSD
* How to include Test Kitchen in a pipeline 
  * [Example](http://hedge-ops.com/cookbook-pipeline-with-jenkinsfile/)
* Basic `kitchen` commands
  * [Knife Subcommands](https://docs.chef.io/knife.html#knife-subcommands)
* Basic `kitchen` configuration
  * [Knife Setup](https://docs.chef.io/knife_setup.html)

# DESCRIBING WHAT CHEF IS
## PRODUCTS AND FEATURES

* The Chef Automate value proposition
  * 
* The Chef Automate features
  * [Chef Automate](https://docs.chef.io/chef_automate.html)
* What the workflow feature is and how it affects productivity What the compliance feature is and how it affects workflow What the visibility feature is and how it affects workflow How a private Supermarket fits into a workflow
* The Chef Automate open source components
  * Chef
  * InSpec
  * Habitat
* What Visibility is
  * [Visibility](https://docs.chef.io/visibility.html)
* What Habitat is
  * [Habitat](https://docs.chef.io/platform_overview.html#habitat)
  * > Habitat offers a new approach to deploying applications called application automation. Application automation means that the automation is packaged with the application and travels with it, no matter where that application is deployed
* What InSpec is
  * [InSpec](https://docs.chef.io/platform_overview.html#inspec)
  * > InSpec is an open-source testing framework with a human- and machine-readable language for specifying compliance, security and policy requirements
  * InSpec [examples](https://github.com/chef/inspec/tree/master/examples)
* What Chef Compliance is
  * [Compliance](https://docs.chef.io/platform_overview.html#compliance)
  * [Overview of Compliance](https://docs.chef.io/chef_automate_compliance.html)
  * identify compliance issues, security risks, and outdated software

## END-TO-END WORKFLOW
* How all Chef products, features and technologies fit together
* The workflow scope
* The compliance scope
* The Chef Automate scope
* How Chef Automate enhances DevOps behaviors
* The aspects of Chef that are relevant to security and compliance teams The aspects of Chef that are relevant to development teams
* The aspects of Chef that are relevant to operations teams
* The aspects of Chef that are relevant to change advisory boards
* How Chef enforces consistency across infrastructure

# DESIGN PHILOSOPHY
## CHEF IS WRITTEN IN RUBY
* How Chef uses a Ruby-based DSL
  * [Chef Style Guide](https://docs.chef.io/ruby.html)
* How to use raw Ruby to extend Chef 
  * [Chef Style Guide](https://docs.chef.io/ruby.html) 
* What a library is
  * [About Libraries](https://docs.chef.io/libraries.html)
  * > A library allows arbitrary Ruby code to be included in a cookbook, either as a way of extending the classes that are built-in to the chef-client—Chef::Recipe, for example—or for implementing entirely new functionality, similar to a mixin in Ruby

 ## EXPLICIT ACTIONS
* How Chef uses explicit actions and only does what you tell it to
  * Chef recipes are declarative
* Actions for common resources such as the :nothing action
	* [Resource Reference](https://docs.chef.io/resource_reference.html)
* What it means to roll back infrastructure
  * Revert to a previous version
* What happens if you reverse the order of resources in a recipe
  * Resources are run in the order they are given
* If Chef can automagically detect what patches should be applied to a system
  * No, it will only do what you explicitly tell it to do

 ## PUSH VS. PULL
* The difference between push and pull models
  * Push based CM: Ansible, Fabric
    * You must have a list of servers to push to
    * Easy to get started
  * Pull based CM: Chef, Puppet, etc
    * Requires a central authority (server, master)
    * Requires a daemon (agent, client, slave) to be installed on all managed machines
* The benefits of a pull model
  * No need to track what machines make up infrastructure
  * No need to track state of machines (Were some machines down when you attempted to apply some changes? Now some machines are in one state while others are in another)
  * Can store configurations
* When a push model is appropriate
  * When your infrastructure is small
  * When installing an agent on a managed machine is not possible (such as a Raspberry Pi)
* What firewall rules need to be enabled for Chef client
  * Port 443 must be open between the client and server
* The Chef client converge intervals and how to invoke immediate updates
  * [The Chef Client Run](https://docs.chef.io/chef_client_overview.html#the-chef-client-run)
  * Use `sudo chef-client` to invoke updates
## RECOMMENDED WORKFLOWS
* What wrapper cookbooks are
  * Add on to original cookbooks. For example, a cookbook that includes (i.e. imports into your custom cookbook) the Nginx cookbook, but adds configurations that are unique to your organization.
* How to use source control, e.g. GitHub 
* How to use the TDD approach
  * [Awesome TDD](https://github.com/unicodeveloper/awesome-tdd)

# CHEF WORKFLOW BASICS
## CONTINUOUS DELIVERY
* What continuous delivery (CD) is 
  * [What is Continuous Delivery](https://continuousdelivery.com)
  * [Continuous Delivery](https://www.chef.io/solutions/continuous-delivery/)
* What role Chef plays in CD
  * Chef Automate provides an automated workflow
  * Encapsulates DevOps complexities
  * Lets you manage infrastructure and application code
* When to run tests
* Why automated configuration management is critical to CD
* Why CD is *more* secure than manual processes

## USING COMPLIANCE TO SCAN
* The benefits of the agentless nature of Chef compliance
  * [Scanner](https://docs.chef.io/automate_compliance_scanner.html) 
* How to check for compliance on nodes that don't have the Chef client installed 
* Basic use cases for compliance
  * [An Overview of Compliance](https://docs.chef.io/chef_automate_compliance.html)
* What language is used to express compliance requirements

## USING CHEF DK TO TEST YOUR CHANGES
* The Test Kitchen value proposition
* Basic use cases for Chef DK
  * creating cookbooks
  * linting
  * unit testing
  * integration testing

## PUBLISHING ARTIFACTS TO CHEF SERVER AND SUPERMARKET
* How to publish artifacts to Chef server
  * using knife (`knife cookbook upload`, `knife role from file ./somerole.json`, etc)
* What Berkshelf is
  * [About Berkshelf](https://docs.chef.io/berkshelf.html)
  * a cookbook dependency manager
* If the Chef Automate workflow feature can push artifacts to things other than a Chef server or Supermarket
* 
* How to manage cookbook dependencies
  * [The Berksfile](https://docs.chef.io/berkshelf.html#the-berksfile)

# UNDERSTANDING BASIC CHEF CODE
## APPROACHABLE CUSTOM CODE
* How to recognize custom code
* How to use libraries How to customize Chef

## APPROACHABLE CHEF CODE
* How to read a recipe that includes the 'package', 'file', and 'service' resources and describe its intent.
