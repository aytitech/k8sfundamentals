# label ve label selector
**label ve label selector** konusuyla ilgili dosyalara buradan erişebilirsiniz.
***
Objelere etiket tanımlama.
```
$ kubectl label "obje_tipi" "obje_ismi" "anahtar=değer"

Ör: kubectl label pods pod9 app=thirdapp
```
***
Objelerden etiket kaldırma.
```
$ kubectl label "obje_tipi" "obje_ismi" "anahtar-"

Ör: kubectl label pods pod9 app-
```
***
Objelere atanmış etiketi güncelleme.
```
$ kubectl label --overwrite "obje_tipi" "obje_ismi" "anahtar=değer"

Ör: kubectl label --overwrite pods pod9 team=team3
```
***
Bir namespace’deki tüm objelere toplu halde label eklemek. 
```
$ kubectl label "obje_tipi" --all "anahtar=değer"

Ör: kubectl label pods --all foo=bar
```
***
Objelere atanmış etiketleri listeleme. 
```
$ kubectl get "obje_tipi" --show-labels

Ör: kubectl get pods --show-labels
```
***
Objeleri belirlenen etiketlere göre listeleme. 

```
$ kubectl get "obje_tipi" -l "anahtar:değer"

Ör: kubectl get pods -l "app"
```
***
Objeleri belirlenen etiketlere göre listeleme. _(virgül **","** **ve**, **"="** **eşittir**, **"!="** **eşit değildir** anlamına gelir. Set-based **"in" içinde**, **"notin" içinde değil** anlamına gelir)_

```
$ kubectl get "obje_tipi" -l "anahtar:değer"

Ör: kubectl get pods -l "app=firstapp,tier=frontend" --show-labels
Ör: kubectl get pods -l "app=firstapp,tier!=frontend" --show-labels
Ör: kubectl get pods -l "app,tier=frontend" --show-labels
Ör: kubectl get pods -l 'app in (firstapp)' --show-labels
Ör: kubectl get pods -l "app=firstapp,app=secondapp" --show-labels
Ör: kubectl get pods -l 'app in (firstapp,secondapp)' --show-labels
Ör: kubectl get pods -l 'app notin (firstapp)' --show-labels
Ör: kubectl get pods -l 'app,app notin (firstapp)' --show-labels
Ör: kubectl get pods -l '!app' --show-labels
Ör: kubectl get pods -l 'app in (firstapp),tier notin (frontend)' --show-labels
```
***