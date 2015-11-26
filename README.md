# -
using UnityEngine;
using System.Collections;

public class Cube : MonoBehaviour 
{
    BoxCollider2D bc2d;
    Animator animator;
    SpriteRenderer cubeImage;
    public  bool go;
    [SerializeField]
    private GameObject cube;
    [SerializeField]
    private Character chara;
	// Use this for initialization
	void Start () 
    {
        animator = cube.GetComponent<Animator>();
        bc2d = cube.GetComponent<BoxCollider2D>();
        cubeImage = cube.GetComponent<SpriteRenderer>();
        bc2d.enabled = false;
        
	}
	
	// Update is called once per frame
	void Update ()   
    { 
        //キャラクターがジャンプとzキーを押してない時
        if (!Character.jump && !chara.cover )
        {
            animator.SetBool("touei", go = Input.GetKey(KeyCode.X));
        }
          
        if (cubeImage.enabled == false)
            bc2d.enabled = false;
	}
    void OnTriggerEnter2D(Collider2D hit)
    {
        //"Respawn"障害物に当たった場合
        if (hit.gameObject.tag == "Respawn")
        {
            //当たったオブジェクトを破壊
            Destroy(hit.gameObject);
            chara.Crow();
        }
    }
    
    
}

