# mods
using UnityEngine;


namespace Mod
{
	public class Mod
	{
		public static void Main()
		{				
			ModAPI.Register(
			    new Modification()
				{
					OriginalItem = ModAPI.FindSpawnable("Pistol"),
					NameOverride = "PISTOL",
					NameToOrderByOverride = "@",
					DescriptionOverride = "",
					CategoryOverride = ModAPI.FindCategory("Firearms"),
					ThumbnailOverride = ModAPI.LoadSprite("icon"),
					AfterSpawn = (Instance) =>
					{
						ModAPI.KeepExtraObjects();
						
						var Slide = Instance.transform.Find("Slide");
                        Slide.GetComponent<SpriteRenderer>().sprite = ModAPI.LoadSprite("bolt.png", 11f);	
					    Slide.GetComponent<SpriteRenderer>().sortingLayerName = "Default";
						Slide.GetComponent<SpriteRenderer>().sortingOrder = -1;
						
						
						Instance.GetComponent<SpriteRenderer>().sprite = ModAPI.LoadSprite("PISTOLSPRITE.png", 11f);
						Instance.GetComponent<SpriteRenderer>().sortingLayerName = "Default";
						Instance.GetComponent<SpriteRenderer>().sortingOrder = -2;
						
						var childObject = new GameObject("ChildObject");
                        childObject.transform.SetParent(Instance.transform);
                        childObject.transform.localPosition = new Vector3(0f, 0f); //offset 
                        childObject.transform.rotation = Instance.transform.rotation;
                        childObject.transform.localScale = new Vector3(1f, 1f);
                        var childSprite = childObject.AddComponent<SpriteRenderer>();
                        childSprite.sprite = ModAPI.LoadSprite("PISTOLFRONT SPRITE.png", 11f);
                        childSprite.sortingLayerName = "Default";
						
						var firearm = Instance.GetComponent<FirearmBehaviour>();
						
						Cartridge customCartridge = ModAPI.FindCartridge("50 AE");																		
						firearm.casingPosition = new Vector3(0f,0.1f);						
						foreach (var c in Instance.GetComponents<Collider2D>())
                        {
                            GameObject.Destroy(c);
						}
                        Instance.AddComponent<BoxCollider2D>();
                        Instance.GetComponent<PhysicalBehaviour>().colliders = Instance.GetComponentsInChildren<Collider2D>();

					    Instance.FixColliders();
						Instance.GetComponent<FirearmBehaviour>().barrelPosition = new Vector2(0.2000f, 0.0900f);
						firearm.ShotSounds = new AudioClip[]
                        {
                            ModAPI.LoadSound("!/pistol1.wav"),
                        };
                        

						
						
			        }
                }
            );
	
			ModAPI.Register(
                new Modification()
                {
                    OriginalItem = ModAPI.FindSpawnable("M1 Garand"),
                    NameOverride = "RIFLE",
                    NameToOrderByOverride = "@",
                    DescriptionOverride = "",
                    CategoryOverride = ModAPI.FindCategory("Firearms"),
                    ThumbnailOverride = ModAPI.LoadSprite("icon"),
                    AfterSpawn = (Instance) =>
                    {
                        ModAPI.KeepExtraObjects(); 
                        var childObject = new GameObject("ChildObject");
                        childObject.transform.SetParent(Instance.transform);
                        childObject.transform.localPosition = new Vector3(0f, 0f); //offset 
                        childObject.transform.rotation = Instance.transform.rotation;
                        childObject.transform.localScale = new Vector3(1f, 1f);
                        var childSprite = childObject.AddComponent<SpriteRenderer>();
                        childSprite.sprite = ModAPI.LoadSprite("GUNSPRTIE BACK.png", 8f); just need copy you gunsprite and name "back" bucause if you dont do that its will be bugged
                        childSprite.sortingLayerName = "Background";                      
						childSprite.sortingOrder = +1;
						
						var Slide = Instance.transform.Find("Slide");
                        Slide.GetComponent<SpriteRenderer>().sprite = ModAPI.LoadSprite("bolt.png", 8f);
                        Slide.GetComponent<SpriteRenderer>().sortingLayerName = "Default";
						 
						
						Instance.GetComponent<SpriteRenderer>().sprite = ModAPI.LoadSprite("GUNSPRITE.png", 8f);
                        Instance.GetComponent<SpriteRenderer>().sortingLayerName = "Default";
						 
                        
                        var firearm = Instance.GetComponent<FirearmBehaviour>();
                        
                        Cartridge customCartridge = ModAPI.FindCartridge("5.56x45mm");
                        
                        firearm.Cartridge = customCartridge;
                        customCartridge.name = "cartridge";                                        
                        customCartridge.Recoil *= 2f;
                        firearm.casingPosition = new Vector3(-0.1f,0.1f);                                                                                            
                       
                        foreach (var c in Instance.GetComponents<Collider2D>())
                        {
                            GameObject.Destroy(c);
                        }
                        Instance.AddComponent<BoxCollider2D>();
                        Instance.GetComponent<PhysicalBehaviour>().colliders = Instance.GetComponentsInChildren<Collider2D>();

                        
                        Instance.FixColliders();
                        Instance.GetComponent<FirearmBehaviour>().barrelPosition = new Vector2(0.7200f, 0.1000f);    postiton where from shoot
                        Instance.GetComponent<FirearmBehaviour>().Automatic = true;
                        Instance.GetComponent<FirearmBehaviour>().AutomaticFireInterval = 0.08f;
                        Instance.GetComponent<FirearmBehaviour>().InitialInaccuracy = 0.0115f;
						firearm.ShotSounds = new AudioClip[]
                        {
                            ModAPI.LoadSound("sound/sound of shoot.mp3"),

                        };
						

						
						
                    }
                }
            );

		}
	}

}	
