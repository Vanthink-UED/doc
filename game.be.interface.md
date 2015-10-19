# 后端游戏接口服务

```javascript

游戏开发接口标准说明
=========================

1. 检测题目是否重复
* url: api/existBasicInfoName
* method: GET
* params: {
    basicinfo_name：string,
    basicinfo_no: int   // 修改时提交
}
* result：{
    errcode: int   // 1：重复，0：不重复
}

2. 创建题目
* url: api/createBasicInfo
* method: POST
* params: {
    basicinfo: {},
    testbanks: []
}
* result：{
    errcode: int,
    basicinfo_no: int
}

3. 更新题目
* url: api/updateBasicInfo
* method: POST
* params: {
    basicinfo: {},
    testbanks: []
}
* result：{
    errcode: int
}

4. 获取题目
* url: api/getBasicInfo
* method: POST
* params: {
    basicinfo_no: int,   // 题目编号
    password: string
}
* result：{
    errcode: int,
    data: {
        basicinfo: {
            is_owner: int,  // 是否为本人创建：1（是），0（否）
            is_pass: int,   // 是否已输入过密码：1（是），0（否）
            is_favorites: int, // 是否已收藏：1（是），0（否）
            ...             // 其他basicinfo表字段数据
        },
        testbanks: []
    }
}

5. 删除题目
* url: api/deleteBasicInfo
* method: GET
* params: {
    basicinfo_no: int   // 题目编号
}
* result：{
    errcode: int    // 0：操作成功
}

6. 查询题目信息
* url: api/searchBasicInfo
* method: GET
* params: {
    page: int,      // 当前页数，默认为1
    size: int,   // 分页条数，默认为10
    type: int,   // 搜索类型，默认为1：1（题目），2（作者）
    keywords: string,   // 搜索关键字，默认为空
    no_password: int    // 是否查看带密码的题目，默认为1：1（仅搜索无密码的题目），0（全部题目）
}
* result：{
    errcode: int,
    data: {
        list: [
            {
                is_owner: int,  // 是否为本人创建：1（是），0（否）
                is_pass: int,   // 是否已输入过密码：1（是），0（否）
                ...             // 其他basicinfo表字段数据
            }
        ],
        count: int    // 总记录数
    }
}

7. 验证密码
* url: api/verifyPassword
* method: POST
* params: {
    basicinfo_no: int,
    password：string
}
* result：{
    errcode: int   // 0：正确，1：错误
}

8. 添加收藏
* url: api/addFavorites
* method: GET
* params: {
    basicinfo_no: int,   // 题目编号
    basicinfo_name: string   // 题目编号
}
* result：{
    errcode: int    // 0：操作成功
}

9. 移出收藏
* url: api/removeFavorites
* method: GET
* params: {
    basicinfo_no: int   // 题目编号
}
* result：{
    errcode: int    // 0：操作成功
}

10. 查询收藏
* url: api/searchFavorites
* method: GET
* params: {
    page: int,      // 当前页数，默认为1
    size: int,   // 分页条数，默认为10
    keywords: string   // 搜索关键字，默认为空
}
* result：{
    errcode: int,
    data: {
        list: [
            {
                basicinfo_no: int,  // 题目编号
                basicinfo_name: string, // 题目名称
                type: int  // 1: 我创建的，2：我收藏的，3：我购买的
            }
            ...
        ],
        count: int    // 总记录数
    }
}

11. 保存成绩
* url: api/saveScore
* method: POST
* params: {
    dtime_start_time: null,         //开始游戏
    dtime_end_time: null,           //结束时间
    char64_activities_time: null,   //活动持续时间
    char64_activities_no: 6,     //活动编号，标识哪个游戏
    char64_testbank_no: 1,       //题目编号
    char64_testbank_name: '',       //题目名称
    char64_testbank_num: 0,      //题目数量，10
    char64_integral: 0,          //积分，做对题目的数量
    char64_stars: 0,             //星星，做题数量
    char64_wrong_num: 0,         //错题，做错数量
    char64_wrong_words: null,       //错题编号，
    char64_homework_no: 0,       //作业编号
    IsRepractice: 0,       //是否重练
    ubint64_score_no: 0     // 成绩编号，重练会添加此成绩编号
}
* result：{
    errcode: int,    // 0：保存成功
    data: {
        integral: int,  // 分数
        stars: int,     // 星星
        score_no: int   // 成绩编号
    }
}

12. 获取排行榜
* url: api/getRankingList
* method: GET
* params: {
    basicinfo_no: int   // 题目编号
}
* result：{
    errcode: int,
    data: [
        {
            is_owner: int,    // 是否本人成绩：1（是），0（否）
            total: int,       // 完成数目
            wrong: int,       // 错误数目
            time: "00:00:00", // 完成时间
            user_name: string,// 用户名
            correct_rate: 0.00  // 正确率
        },
        ...
    ]
}
```