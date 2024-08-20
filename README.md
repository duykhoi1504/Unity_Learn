using System.Collections;
using System.Collections.Generic;
using TMPro;
using UnityEngine;
using UnityEngine.UI;

public class PlayerStatsUpgradeDisplay : MonoBehaviour
{
    // Start is called before the first frame update
    Button button;
    [SerializeField] TextMeshProUGUI coinText, valueText, labelText;
    [SerializeField] GameObject purchaseText;

    int coinCard;
    float valueCard;
    private void Awake() {
        button = GetComponent<Button>();
    }
    private void Start() {
        
         button.onClick.AddListener(SelectPlayerStatsCard);
    }
    // private void Update()
    // {
    //     button.onClick.AddListener(() => SelectPlayerStatsCard());
    // }

    public void UpgradePlayerStatsButtonDisplay(int coin, float value, bool isMax, string name)
    {

        labelText.text = name;

        coinText.text = coin.ToString();
        valueText.text = value.ToString();
        purchaseText.SetActive(!isMax);
        coinCard = coin;
        valueCard = value;

    }

    public void SelectPlayerStatsCard()
    {
        PlayerCoin.Instant.CurrentCoin -= coinCard;
        GameManager.Instance.ChangeState(GameState.GAMEPLAY);

    }
}
