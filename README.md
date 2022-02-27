Código do Player:
*
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Player1 : MonoBehaviour
{
    public Animator anim;
    public float speed;

    public GameObject ProgetelV;

    // Update is called once per frame
    void Update()
    {
        Shoot();

        Vector3 movement = new Vector3(Input.GetAxis("Horizontal"), Input.GetAxis("Vertical"), 0f);

        anim.SetFloat("Horizontal", movement.x);
        anim.SetFloat("Vertical", movement.y);
        anim.SetFloat("Speed", movement.magnitude);

        transform.position = transform.position + movement * speed * Time.deltaTime;
    }

    void Shoot()
    {
        if (Input.GetKeyDown(KeyCode.E))
            Instantiate(ProgetelV, this.transform.position, this.transform.rotation);
        
    }
}
*

Código do Projetil:
*
using UnityEngine;

public class BulletRed : MonoBehaviour
{
    const float lifeTime = 1;
    public float speed;

    // Start is called before the first frame update
    void Start()
    {
        Destroy(this.gameObject, lifeTime);        
    }

    // Update is called once per frame
    void Update()
    { 
        transform.Translate(Vector2.down * speed * Time.deltaTime);
    }

    private void OnTriggerEnter2D(Collider2D collision)
    {
        
        if (collision.gameObject.tag.Equals("Player"))
        {
            return;
        }
        if (collision.gameObject.tag.Equals("Player2"))
        {
            var Player2Obj = collision.GetComponent<VidaAzul>();
            Player2Obj.TomaDano(1);
        }
        Destroy(gameObject);
    }



}
*
E o código da Vida:
*
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class VidaVermelha : MonoBehaviour
{
    [SerializeField]
    private int _vida = 20;
    
    public void TomaDano(int dano)
    {
        _vida -= dano;

        if(_vida <= 0)
        {
            Morre();
        }
    }
    private void Morre()
    {
        Destroy(gameObject);
    }

}
*

<!---
Mickel0/Mickel0 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
