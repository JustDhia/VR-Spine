# VR Spine

Le but de ce projet est de concevoir et d’implémenter une plateforme de suivi de la scoliose idiopathique en 3D, le projet fait partie du module VR/AR (module optionnel de la formation SIQ à l'Ecole Superieure d'Informatique d'Alger).

# Techno
* Unity 3D [2018.4.23f1]
* C#

# Fonctionnalités 
* UI
* Prédiction des états intermédiaires du scoliose
* Calcule de l'angle Cobb

# Architecture du projet
Le projet est constitué de 4 scenes, la scene principale (Main Menu) et 3 scenes pour les trois patients.
# Éléments clés du projet
## 1 - Le script ChangeStateWithController
Le script est attaché aux objets (vertébrés) pour assurer le changement d’état
```
public class ChangeStateWithSlider : MonoBehaviour
{
    public Slider slider;
    public Transform SecondPosition;

    private Vector3 position1;
    private Vector3 position2;

    private Vector3 rotation1;
    private Vector3 rotation2;

    void Start() {   
        position1 = this.transform.position;
        position2 = SecondPosition.position;

        rotation1 = this.transform.eulerAngles;
        rotation2 = SecondPosition.transform.eulerAngles;

        slider.onValueChanged.AddListener(UpdatePosition);
    }

    void UpdatePosition(float value) {
        Vector3 newPosition = Vector3.LerpUnclamped(position1, position2, value);
        this.transform.position = newPosition;
        float angle = Mathf.LerpAngle(rotation1.z, rotation2.z, value);
        this.transform.eulerAngles = new Vector3(0, 0, angle);
    }
}
```
# 2 - Le script CobbCalculator
Calculer l'angle Cobb entre 2 vertèbres
```
public class CobbCaclulator : MonoBehaviour {   
    public Text cobbText;
    public InputField Vert1;
    public InputField Vert2; 
    private float x1;
    private float x2;
    private float cobb;
    private float angle;
    
    void Start() {}
    void Update() {
        x1 = GameObject.Find(Vert1.text).transform.localEulerAngles.z;
        if (x1> 180f) {
            x1 = 360f - x1;}
        x2 = GameObject.Find(Vert2.text).transform.localEulerAngles.z;
        if (x2> 180f) {
            x2 = 360f - x2;}
        angle = x1-x2;
        if (angle<0) {
            angle = -angle;}
        cobb = 360 - (360 - 180 - angle * 2) *2; 
        cobbText.text = cobb.ToString();
    }
}
```

License
----

MIT

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)


   [dill]: <https://github.com/joemccann/dillinger>
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>
