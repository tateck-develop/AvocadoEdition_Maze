# AvocadoEdition_Maze
아보카도 에디션 플러그인 : 미궁
---
미궁 진행률 적용 방법



캐릭터 프로필 페이지 (view.ing.pgp) 에 적용 시 $mb['mb_maze'] 를 사용해주세요.
현재 로그인 중인 계정에 대해 미궁 진행도를 표기하고 싶을 땐 **$mb['mb_maze']를 -> $member['mb_maze']**로 변경하여 를 사용하실 수 있습니다.
캐릭터가 생성된 계정에 대해서만 랭킹 기록이 보관됩니다.

### 추가 코드
```
<?
$maze_count = sql_fetch("select count(*) as cnt from {$g5['maze_table']}");
$maze_count = $maze_count['cnt'];
$ma = sql_fetch("select ma_subject, ma_order from {$g5['maze_table']} where ma_id = '{$mb['mb_maze']}'");
$ma_count = sql_fetch("select count(*) as cnt from {$g5['maze_table']} where ma_order <= '{$ma['ma_order']}' and ma_id != '{$mb['mb_maze']}'");
$ma_count = $ma_count['cnt'];
$ma_per = $ma_count == 0 ? 0 : $ma_count / $maze_count * 100;

/* 진행률 그래프 출력 예시
<dl>
	<dt>Maze</dt>
	<dd>
		<p>
			<i><?=$ma['ma_subject'] ? $ma['ma_subject']." 진행중" : "..."?></i>
			<span style="width: <?=$ma_per?>%;"></span>
			<sup style="width: <?=$ma_per?>%;"></sup>
		</p>
	</dd>
</dl>
*/
?>
<p>미궁 - <?=$ma['ma_subject']?> 진행중</p>
```

copyright by.AvocadoEdition
https://avocado-edition-rout.postype.com/