Powershell Cookbook
===================
[![Build Status](https://travis-ci.org/chef-cookbooks/powershell.svg?branch=master)](http://travis-ci.org/chef-cookbooks/powershell)
[![Cookbook Version](https://img.shields.io/cookbook/v/powershell.svg)](https://supermarket.chef.io/cookbooks/powershell)

Installs and configures PowerShell 2.0, 3.0, 4.0 or 5.0.

For users of Chef 10 without the `powershell_script` built-in resource, this cookbook also includes a resource/provider for executing scripts using the PowerShell interpreter.

Requirements
------------

### Platforms

Not every version of Windows supports every version of Powershell. The following table illustrates Powershell support across the Windows family. **Included** means that the base installation of the operating system includes the indicated version of Powershell.

<table>
  <tr>
    <th>Windows Version</th>
    <th>PowerShell 2.0</th>
    <th>PowerShell 3.0</th>
    <th>PowerShell 4.0</th>
    <th>PowerShell 5.0</th>
  </tr>
  <tr>
    <td>Windows Server 2008 R2</td>
    <td>Included</td>
    <td>Supported</td>
    <td>Supported</td>
    <td></td>
  </tr>
  <tr>
    <td>Windows Server 2012 / Windows 8</td>
    <td>Supported</td>
    <td>Included</td>
    <td>Supported</td>
    <td></td>
  </tr>
  <tr>
    <td>Windows Server 2012R2 / Windows 8.1</td>
    <td></td>
    <td></td>
    <td>Included</td>
    <td>Supported</td>
  </tr>
  <tr>
    <td>Windows Server 2016 TP4 / Windows 10</td>
    <td></td>
    <td></td>
    <td>/td>
    <td>Included</td>
  </tr>
</table>

### Cookbooks

* windows

PowerShell also requires the appropriate version of the Microsoft .NET Framework to be installed, if the operating system does not ship with that version. The following community cookbooks are used to install the correct version of the .NET Framework:

* ms_dotnet

Resource/Provider
-----------------

### `powershell_module`

Installs or uninstalls a Powershell module. You either need to install rubyzip with chef_gem or
include the default recipe before using this resource.

#### Actions

- :install: install the powershell module
- :uninstall: uninstall the powershell module

#### Attribute Parameters

- `name`: name attribute. Name of the module to install or uninstall.
- `source`: quoted string of Local directory path(Not zipfile) or URL for the zipped module folder.
- `package_name`: quoted string of name of the module to install or uninstall.
- `destination`: location where module should be installed

#### Examples

```ruby
include_recipe 'powershell::default'

# Install module from local directory path
# change the package_name and source
powershell_module "PsUrl" do
  package_name "PsUrl"
  source "C:\\PsUrl"
end
```

```ruby
# Install from URL of zipped module folder
powershell_module "posh-git" do
  package_name "posh-git"
  source "https://github.com/dahlbyk/posh-git/zipball/master"
end
```

```ruby
# change the package_name
powershell_module "Uninstall PsUrl" do
  package_name "PsUrl"
  action :uninstall
end
```

```ruby
# Install without using 'source' attribute
powershell_module "https://github.com/dahlbyk/posh-git/zipball/master" do
  package_name "posh-git"
end
```

Usage
-----

**Note**: The installation may require a restart of the node being configured before PowerShell can be used.

### default

The default recipe is needs to be included before using the powershell_module resource.

### powershell2

Include the `powershell2` recipe in a run list, to ensure PowerShell 2.0 is installed.

On the following versions of Windows the PowerShell 2.0 package will be downloaded from Microsoft and installed:

- Windows XP
- Windows Server 2003
- Windows Server 2008
- Windows Vista

On the following versions of Windows, PowerShell 2.0 is present and must just be enabled:

- Windows 7
- Windows Server 2008 R2
- Windows Server 2008 R2 Core

### powershell3

Include the `powershell3` recipe in a run list, to install PowerShell 3.0 is installed on applicable platforms. If a platform is not supported or if it already includes PowerShell 3.0, an exception will be raised.

### powershell4

Include the `powershell4` recipe in a run list, to install PowerShell 4.0 is installed on applicable platforms. If a platform is not supported or if it already includes PowerShell 4.0, an exception will be raised.

### powershell5

Note: Windows Management Framework 5 is in preview.

Include the `powershell5` recipe in a run list, to install PowerShell 5.0 is installed on applicable platforms. If a platform is not supported or if it already includes PowerShell 5.0, an exception will be raised.

References
----------

* Installing [Windows Management Framework 2.0](http://support.microsoft.com/kb/968929)
* Installing [Windows Management Framework 3.0](http://www.microsoft.com/en-us/download/details.aspx?id=34595)
* Installing [Windows Management Framework 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855)
* Installing [Windows Management Framework 5.0](http://www.microsoft.com/en-us/download/details.aspx?id=42936)

License & Authors
-----------------

- Author:: Seth Chisamore (<schisamo@chef.io>)
- Author:: Julian Dunn (<jdunn@chef.io>)

```text
Copyright:: 2011-2015, Chef Software, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
