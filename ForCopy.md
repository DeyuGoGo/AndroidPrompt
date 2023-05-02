你參考一下新的suspect 的資料結構。

data class Suspect(
    val accessories: String,
    val alibi: String,
    val clothing: String,
    val motive: String,
    val name: String,
    val questions: List<Question>,
)
data class Question(
    val answer: String,
    val question: String
)


 items(gameData.suspects) { s ->
                        Spacer(modifier = Modifier.height(8.dp))
                        SuspectCard(
                            suspect = s,
                            modifier = Modifier
                                .fillMaxWidth()
                                .shadow(2.dp, MaterialTheme.shapes.medium),
                            onClick = {
                                gameViewModel.sendIntent(GameIntent.GuessSuspect(suspect = s))
                            }
                        )
                    }


@Composable
fun SuspectCard(suspect: Suspect, onClick: () -> Unit, modifier: Modifier) {
    Card(
        modifier = modifier
            .fillMaxWidth()
            .padding(8.dp)
            .clip(RoundedCornerShape(8.dp))
            .clickable { onClick() },
        elevation = 4.dp,
        backgroundColor = MaterialTheme.colors.surface
    ) {
        Column(
            modifier = Modifier
                .padding(16.dp)
                .animateContentSize()
        ) {
            Text(
                text = "嫌疑人: ${suspect.name}",
                style = MaterialTheme.typography.h6
            )
            Spacer(modifier = Modifier.height(8.dp))
            Text(
                text = "服裝: ${suspect.clothing}",
                style = MaterialTheme.typography.body1
            )
            Text(
                text = "配件: ${suspect.accessories}",
                style = MaterialTheme.typography.body1
            )
            Text(
                text = "不在場證明: ${suspect.alibi}",
                style = MaterialTheme.typography.body1
            )
            Text(
                text = "動機: ${suspect.motive}",
                style = MaterialTheme.typography.body1
            )
        }
    }
}


幫我把這個列表按下去可以show一個跳窗，可以選擇詢問嫌疑人或者猜他是兇手，選取過的問題跟答案要秀出來，設計好看一點，謝謝