it('Navigate to My balances and verify the balances', async function () {
    await homePage.retry();

    // 滑动到余额区域
    await touchActions.swipeToView(homePage.lbMyCombinedBalancesOwned());

    // 获取所有 TextView 元素（假设这些是余额项）
    const children = await $$('//android.widget.TextView');
    const total = children.length;
    console.log('Number of child elements:', total);

    // 获取第一个余额文本
    const currencyAmount = await (await homePage.lbMyBalancesOwned()).getText();
    console.log("Balance number I own is: " + currencyAmount);

    // 验证是否包含美元符号
    assert.isTrue(currencyAmount.includes('$'), 'Currency amount should contain $');

    await screenShot(this.test);

    // 继续往下滑动查看欠款余额
    await touchActions.swipeUp();

    // 验证欠款余额是否存在
    if (await (await homePage.lbMyBalancesOwed()).isExisting()) {
        let owedAmount = await (await homePage.lbMyBalancesOwed()).getText();
        console.log("Balance I owe is: " + owedAmount);

        assert.isTrue(owedAmount.includes('$'), 'Owed amount should contain $');
        await screenShot(this.test);
    } else {
        console.log("No owed balance element found.");
    }
});
