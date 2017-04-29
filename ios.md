# iOS Development
## Project setup 
When setting up a new project a numerous things have to be properly set to avoid problems with application publishing to App Store with the importance on code and compiler settings to be matching across the whole development team. To avoid manually setting every single Xcode project we use [Liftoff](https://github.com/liftoffcli/liftoff) to seamlessly create unified projects.
### Liftoff installation
#### Requirements
Installation of Liftoff is handled by [Homebrew](https://brew.sh) and needs to be installed in order to install Liftoff.
### Installation
Before installation take a look at [Requirements](###requirements). 

To install Liftoff run following commands in Terminal.

```
brew tap thoughtbot/formulae
brew install liftoff
```
### Configuration
Liftoff can be configured using a liftoffrc file located in `./.liftoffrc` or `~/.liftoffrc`.
To obtain default configuration used in Enrian run following commands in Terminal:

```
cd ~/<Your Developer Folder>/<Your Enrian Dev Folder>/
git clone git@github.com:enrian/liftoff-configuration.git
```

Enrian defaults have following configuration:

- Company name and company identifier
- Prefix set to empty string
- Test target name
- Warning as errors set to false
- Disable default git configuration from liftoff
- Disable settings from liftoff
- Turn off run scripts
- Set up Swift as a default project template
- Use CocoaPods with default Podfile
- Initial Git repository and add default `README.md` and `.gitignore`
- An initial commit is made 

For more see [Enrian Liftoff Configuration]().

### Usage
To use Liftoff for creating new projects run `liftoff` command in your `~/<Your Developer Folder>/<Your Enrian Dev Folder>/`.

```
cd ~/<Your Developer Folder>/<Your Enrian Dev Folder>/
liftoff
```

When prompeted:

- enter new project name (e.g. **TestApp**)
- enter prefix in the format: **EPTA** (**E**nrian **P**artners **T**est **A**pp)

After liftoff creates a project a Xcode will be opened with the newly created project. If prompted convert the project to the latest Swift syntax and then navigate to **TestApp** / **Targets** / TestApp, select **General** tab and in the **Signing** section for the option **Team** select Enrian Partners, s.r.o.

![Signing](./ios-docs/img/signing.png)

#### Project Warnings
After using a Liftoff for creating a project a warning can be shown after the creation with suggestion to enable recommended compiler/project settings. Proceed with **Perform Changes** as current Liftoff configuration does not include latest LLVM compiler flags. 

## Automating deployment 
TODO
