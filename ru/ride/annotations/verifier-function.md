# Функция-верификатор

Функция-верификатор — функция [dApp-скрипта](/blockchain/dapp-script.md) с аннотацией [@Verifier](/ru/ride/annotations.md).

Функция-верификатор отвечает за [валидацию транзакций](/ru/blockchain/transaction-validation.md) и ордеров, которые отправляются с [dApp](/blockchain/dapp.md).

У dApp-скрипта может быть только _одна_ функция-верификатор.

Функция-верификатор не имеет аргументов.

## Пример

``` ride
{-# STDLIB_VERSION 3 #-}
{-# CONTENT_TYPE DAPP #-}
{-# SCRIPT_TYPE ACCOUNT #-}
 
@Verifier(tx)
func verify() = {
    match tx {
        case _: Order|SetScriptTransaction =>
            sigVerify(tx.bodyBytes, tx.proofs[0], tx.senderPublicKey)
        case _ => false
    }
}
```