<?php

/**
 * Created by IntelliJ IDEA.
 * User: wangchao
 * Date: 1/9/17
 * Time: 9:46 PM
 */
class ErrorCode
{
    /**
     * 普通错误
     */
    const ERROR = -1;

    /**
     * 内部 API 参数格式错误
     */
    const API_PARAM_ERROR = 1000;

    /**
     * 网关 API 参数错误
     */
    const GATEWAY_API_PARAM_ERROR = 1001;

    /**
     * 权限错误
     */
    const API_NOAUTH = 1300;

    /**
     * 卖家权限错误
     */
    const API_NOAUTH_SELLER = 1301;

    /**
     * 会员权限错误
     */
    const API_NOAUTH_MEMBER = 1302;

    /**
     * 安全错误
     */
    const SECURE_ERROR = 1500;

    /**
     * 安全错误，尝试密码失败次数太多
     */
    const SECURE_ERROR_TRY_TOO_MANY_PASSWORD = 1501;

    /**
     * 系统错误
     */
    const SYSTEM_ERROR = 1700;

    /**
     * 系统错误，无法写SESSION
     */
    const SYSTEM_ERROR_CANT_WRITE_SESSION = 1701;
    /**
     * 系统错误，无法写MYSQL
     */
    const SYSTEM_ERROR_CANT_WRITE_MYSQL = 1702;
    /**
     * 系统错误，无法写MEMCACHE
     */
    const SYSTEM_ERROR_CANT_WRITE_MEMCACHE = 1703;
    /**
     * 系统错误，无法写REDIS
     */
    const SYSTEM_ERROR_CANT_WRITE_REDIS = 1704;

    /**
     * 系统错误，不是有效API名
     */
    const SYSTEM_ERROR_NOT_VALID_API_NAME = 1710;


    /**
     * 系统错误，不是有效API名
     */
    const SYSTEM_ERROR_SQL_ORDER_TYPE = 1720;


    /**
     * 邮件格式错误
     */
    const EMAIL_FORMAT_ERROR = 1901;

    /**
     * 用户授信凭证错误
     */
    const USER_CREDENTIALS_ERROR = 2001;


    /**
     * @param array $ret
     * @return bool
     */
    public function checkErrorCodeConflict(&$ret = [])
    {
        $constants = self::getConstants();
        $flippedConstants = array_flip($constants);

        if (count($flippedConstants) != count($constants)) {
            $codesMap = [];
            foreach ($constants as $const => $code) {
                if (in_array($code, $codesMap)) {
                    $ret[] = [
                        'code' => $code,
                        'const' => $const,
                    ];
                } else {
                    $codesMap[] = $code;
                }
            }
            return false;
        }

        return true;

    }

    static function getConstants()
    {
        $oClass = new ReflectionClass(__CLASS__);
        return $oClass->getConstants();
    }

    public function documentGenerate($exportJsonFile = false)
    {
        $constants = self::getConstants();

        $phpCode = file_get_contents(__FILE__);
        $phpCode = str_replace("\n", "", $phpCode);

        $result = [];
        foreach ($constants as $const => $code) {
            $patten = "!\{.*\/\*\*(.*)\*\/.*const " . $const . "[ |=]!u";
            preg_match_all($patten,
                $phpCode,
                $out, PREG_PATTERN_ORDER);
            unset($out[0]);

            if (isset($out[1][0])) {
                $comment = trim($out[1][0]);
                $comment = str_replace("*", "", $comment);

                $result[] = [
                    "code" => $code,
                    "desc" => trim($comment)
                ];
            }
        }

        if ($exportJsonFile) {
            file_put_contents(__DIR__ . "/error_code.json", json_encode($result));
        }
        return $result;
    }
}

