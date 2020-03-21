# Self Signed Certificates demo Android | Cordova

Demo of how to configure custom trust anchors with network security configuration.

Demo includes 3 commits,
1. [Basic cordova project](https://github.com/devzeze/cordova_selfsigned/commit/9ec8de71c20a8ac20707042d7e22480e15d68648)
2. [Add a call to a self signed certificate](https://github.com/devzeze/cordova_selfsigned/commit/cc0beb89f685c8a92d7be5eca7c5a147b8c62ea6)
3. [Add CA to custom trusted authorities](https://github.com/devzeze/cordova_selfsigned/commit/bf31570240deb79f407e8d6e88652d545959fd96)


## References

The self signed certificate used is from https://self-signed.badssl.com/

To get the certificate to use in step 3:

```
> openssl s_client -connect self-signed.badssl.com:443 -showcerts
```

Documentation of implementation can be found here:

[Android - Network security configuration
](https://developer.android.com/training/articles/security-config)

## Implementation
Implementation includes:

1. Store the certificate in ./android/app/src/main/res/raw/<trusted_cert>

2. Create an xml file in ./android/app/src/main/res/xml/network_security_config.xml
with content:
```
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <base-config cleartextTrafficPermitted="true">
        <trust-anchors>
            <certificates src="@raw/<trusted_cert>" />
        </trust-anchors>
    </base-config>
</network-security-config>
```

3. Add network config to AndroidManifest file in root of Android platform
```
<application
...
android:networkSecurityConfig="@xml/network_security_config"
...
>
```

## Authors

* **devzeze** -[GitHub](https://github.com/devzeze)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details
