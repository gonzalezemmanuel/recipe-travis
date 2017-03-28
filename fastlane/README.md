fastlane documentation
================
# Installation

Make sure you have the latest version of the Xcode command line tools installed:

```
xcode-select --install
```

## Installation method:

<table width="100%" >
<tr>
<th width="33%">Rubygems</td>
</tr>
<tr>
<td width="33%" align="center">macOS or Linux with Ruby 2.0.0 or above</td>
</tr>
<tr>
<td width="33%" align="center"><code>sudo gem install fastlane -NV</code></td>
</tr>
</table>
# Available Actions
### increment
Take the lastest build number uploaded on testflight ans add 1 to it. This avoids to upload an ipa with the same build number. 

```
fastlane increment
```

### upload
Upload to testflight the generated ipa by [travis](../scritps/distribution-deploy)

```
fastlane upload
```


----
