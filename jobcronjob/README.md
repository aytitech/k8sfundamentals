# Job ve CronJob
**job ve cronjob** konusuyla ilgili dosyalara buradan erişebilirsiniz.
***
Job objelerinin listelenmesi

```
$ kubectl get job
```
***
Job objelerinin silinmesi

```
$ kubectl delete job "job_ismi

Ör: kubectl delete job myjob
```
***
CronJob objelerinin listelenmesi

```
$ kubectl get cronjob
```
***
CronJob objelerinin silinmesi

```
$ kubectl delete cronjob "cronjob_ismi

Ör: kubectl delete cronjob mycronjob
```