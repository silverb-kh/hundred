# 고도몰 쇼핑몰 관리자 상품 검색 고도화 

복수 검색 허용 (상품코드, 자체 상품코드)

## 작업 위치 결정
---

* goods/goods_list.php 에서 아래와 같이 공통 템플릿을 사용하는 것을 확인
```
 	<?php include($goodsSearchFrm); ?> 
```

* controller/admin/goods/goodsListController.php 에서 아래와 같이 관리자 디자인 템플릿 선언
```
$this->getView()->setDefine('goodsSearchFrm',  Request::getDirectoryUri() . '/goods_list_search.php');
```

* Component/Goods/GoodsAdmin -> getAdminListGoods($mode, $pageNum)
* Component/Goods/GoodsAdmin -> setSearchGoods($getValue)


## 작업 내용
---

상위 메서드(setSearchGoods)를 덮어쓰기(overwrite)하고 아래 항목을 수정합니다. 
```
else if($this->search['key'] == 'goodsNo'){	//@inwarde - full match check
	$keyword_arr = explode (",", $this->search['keyword']);
	$gNoStr = 'g.goodsNo IN (';
	foreach ($keyword_arr as $keyword) {
		$gNoStr .= ' ?, ';
		$this->db->bind_param_push($this->arrBind, $fieldTypeGoods[$this->search['key']], trim($keyword));
	}
	$gNoStr = rtrim($gNoStr, ", ");
	$gNoStr .= ')';
	$this->arrWhere[] = $gNoStr;
	// echo $gNoStr;
}
```