Thanks for helping make GitHub safe for everyone.

## Security

GitHub takes the security of our software products and services seriously, including all of the open source code repositories managed through our GitHub organizations, such as [GitHub](https://github.com/GitHub).

Even though [open source repositories are outside of the scope of our bug bounty program](https://bounty.github.com/index.html#scope) and therefore not eligible for bounty rewards, we will ensure that your finding gets passed along to the appropriate maintainers for remediation. 

## Reporting Security Issues

If you believe you have found a security vulnerability in any GitHub-owned repository, please report it to us through coordinated disclosure.

**Please do not report security vulnerabilities through public GitHub issues, discussions, or pull requests.**

Instead, please send an email to opensource-security@github.com.

Please include as much of the information listed below as you can to help us better understand and resolve the issue:

  * The type of issue (e.g., buffer overflow, SQL injection, or cross-site scripting)
  * Full paths of source file(s) related to the manifestation of the issue
  * The location of the affected source code (tag/branch/commit or direct URL)
  * Any special configuration required to reproduce the issue
  * Step-by-step instructions to reproduce the issue
  * Proof-of-concept or exploit code (if possible)
  * Impact of the issue, including how an attacker might exploit the issue

This information will help us triage your report more quickly.

## Policy

See [GitHub's Safe Harbor Policy](https://docs.github.com/en/site-policy/security-policies/github-bug-bounty-program-legal-safe-harbor#1-safe-harbor-terms)
{
  "name": "gubon-production-validation",
  "version": "1.0.0",
  "private": true,
  "type": "module",
  "engines": {
    "node": ">=20"
  },
  "scripts": {
    "split": "node scripts/split.mjs",
    "normalize": "node scripts/normalize.mjs",
    "typecheck": "tsc --noEmit",
    "build": "tsc",
    "validate": "node scripts/validate.mjs",

    "bootstrap": "npm run split && npm run normalize && npm run typecheck && npm run build && npm run validate",

    "dev": "vite",
    "preview": "vite preview --host 0.0.0.0",

    "convert": "node scripts/convert.mjs",
    "convert:preview": "node scripts/convert-preview.mjs",

    "test:e2e": "playwright test",
    "test:stress": "node scripts/webhook-stress-test.mjs",
    "test:chaos": "node scripts/chaos-test.mjs",

    "validate:tac": "node scripts/generate-tac-results.mjs",
    "generate:evidence": "node scripts/generate-evidence.mjs",
    "generate:report": "node scripts/generate-report.mjs",
    "package:evidence": "node scripts/package-evidence.mjs",

    "validate:production": "npm run bootstrap && npm run test:e2e && npm run test:stress && npm run test:chaos && npm run validate:tac && npm run generate:evidence && npm run generate:report && npm run package:evidence"
  }
}

npm run validate:production

SOURCE
  ↓
PARSE
  ↓
CLASSIFY
  ↓
SPLIT
  ↓
GENERATE FILES
  ↓
NORMALIZE
  ↓
TYPECHECK
  ↓
BUILD
  ↓
E2E
  ↓
WEBHOOK STRESS
  ↓
CHAOS
  ↓
TAC ENGINE
  ↓
EVIDENCE
  ↓
REPORT
  ↓
PDF
  ↓
PACKAGE
  ↓
PRODUCTION VERDICT

artifacts/
├── E2E_Report.md
├── E2E_Report.pdf
├── TAC_Matrix.csv
├── tac_results.json
├── test-results.json
├── stress-results.json
├── chaos-results.json
├── audit-chain.json
├── compensation-log.json
├── webhook-results.json
├── metrics/
│   └── latency.png
├── logs/
│   ├── application.log
│   ├── webhook.log
│   ├── redis-lock.log
│   └── compensation.log
└── EvidencePackage.zip

const tacChecks = [
  {
    id: "TAC-A1",
    description: "Webhook Signature Verification",
    validate: data => data.signatureVerified === true
  },
  {
    id: "TAC-A2",
    description: "Replay Protection",
    validate: data => data.duplicateLedgerEntries === 0
  },
  {
    id: "TAC-A3",
    description: "Idempotency",
    validate: data => data.idempotencyViolations === 0
  },
  {
    id: "TAC-B1",
    description: "Redis Lock",
    validate: data => data.redisLockViolations === 0
  },
  {
    id: "TAC-C1",
    description: "Payment State Integrity",
    validate: data => data.invalidPaymentTransitions === 0
  },
  {
    id: "TAC-D1",
    description: "Audit Chain",
    validate: data => data.auditChainValid === true
  },
  {
    id: "TAC-E1",
    description: "Entitlement Integrity",
    validate: data => data.invalidEntitlements === 0
  },
  {
    id: "TAC-F1",
    description: "Recovery",
    validate: data => data.unrecoveredFailures === 0
  }
];

const results = tacChecks.map(check => ({
  id: check.id,
  description: check.description,
  status: check.validate(testData) ? "PASS" : "FAIL"
}));

const failed = results.filter(result => result.status === "FAIL");

if (failed.length > 0) {
  process.exitCode = 1;
}

REQUEST_ID
    ↓
SESSION_ID
    ↓
DECISION_ID
    ↓
INPUT_SNAPSHOT
    ↓
DECISION_VECTOR
    ↓
REPORT_ID
    ↓
ORDER_ID
    ↓
PAYMENT_ID
    ↓
WEBHOOK_EVENT_ID
    ↓
ENTITLEMENT_ID
    ↓
FULFILLMENT_ID
    ↓
NOTIFICATION_ID
    ↓
OUTCOME_ID
    ↓
REVENUE_LEDGER_ID

name: GUBON Production Validation

on:
  workflow_dispatch:
  push:
    branches:
      - main

jobs:
  production-validation:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm

      - name: Install
        run: npm ci

      - name: Bootstrap
        run: npm run bootstrap -- input/gubon-source.txt

      - name: E2E
        run: npm run test:e2e

      - name: Webhook Stress
        run: npm run test:stress

      - name: Chaos
        run: npm run test:chaos

      - name: TAC Validation
        run: npm run validate:tac

      - name: Generate Evidence
        run: npm run generate:evidence

      - name: Generate Report
        run: npm run generate:report

      - name: Package Evidence
        run: npm run package:evidence

      - name: Upload Evidence
        uses: actions/upload-artifact@v4
        with:
          name: gubon-evidence-package
          path: artifacts/EvidencePackage.zip

SOURCE
 ↓
BUILD
 ↓
TYPECHECK
 ↓
E2E PASS
 ↓
STRESS PASS
 ↓
CHAOS PASS
 ↓
TAC PASS
 ↓
EVIDENCE GENERATED
 ↓
REPORT GENERATED
 ↓
EVIDENCE PACKAGE GENERATED
 ↓
RELEASE

FAIL
 ↓
STOP
 ↓
NO RELEASE
 ↓
NO PRODUCTION CLAIM

PRODUCTION RELEASE
        ↓
REAL USER
        ↓
REAL TRANSACTION
        ↓
FIRST COMMERCIAL TRANSACTION

zip -r EvidencePackage.zip artifacts/這套設計將「Skills 建制與動態分配」正式納入資料庫結構與 Kernel 派工邏輯中。Kernel 不僅是審查官，更是技能註冊庫（Skill Registry）的最高調度官，能隨時註冊新 Skill、掛載/卸載職人，並針對每次決策進行精準分配。
Prisma Schema 新增 Skills 註冊與分配表
// 新增至 prisma/schema.prisma

// 1. 技能與職人建制庫 (Skill Registry)
model Skill {
  id          String                 @id @default(uuid())
  code        String                 @unique // 例如：CRAFTSMAN_01_TECH, SKILL_CASHFLOW
  name        String                 // 技能名稱：技術手、金流手、法務手...
  groupTag    String                 // 一組(前端體驗) | 二組(後端架構)
  description String?
  isActive    Boolean                @default(true) // 熱插拔開關：true=啟用, false=停用
  createdAt   DateTime               @default(now())
  updatedAt   DateTime               @updatedAt
  allocations SessionSkillAllocation[]
}

// 2. Kernel 決策會話派工紀錄 (Session Skill Allocation)
model SessionSkillAllocation {
  id         String          @id @default(uuid())
  sessionId  String
  session    DecisionSession @relation(fields: [sessionId], references: id)
  skillId    String
  skill      Skill           @relation(fields: [skillId], references: id)
  status     String          @default("DISPATCHED") // DISPATCHED | EVIDENCE_SUBMITTED | REJECTED
  assignedAt DateTime        @default(now())
}

GUBON Kernel 動態分配與派工邏輯 (TypeScript)
// packages/kernel/src/KernelSkillAllocator.ts

import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient();

export interface SkillDispatchPlan {
  sessionId: string;
  selectedSkillCodes: string[];
  allocatedSkillIds: string[];
}

export class KernelSkillAllocator {
  /**
   * Kernel 最高統帥：評估決策情境，從 active Skills 庫中挑選並綁定派工紀錄
   */
  public static async allocateSkillsForSession(
    sessionId: string,
    problemCategory: number
  ): Promise<SkillDispatchPlan> {
    // 1. 撈取資料庫中所有啟用的 (isActive = true) Skills
    const activeSkills = await prisma.skill.findMany({
      where: { isActive: true },
    });

    // 2. Kernel 根據分類進行動態派工匹配
    const targetCodes: string[] = ['CRAFTSMAN_01_TECH', 'CRAFTSMAN_02_ARCHITECT'];

    if (problemCategory === 2) {
      targetCodes.push('CRAFTSMAN_04_PROFIT', 'CRAFTSMAN_08_CASHFLOW');
    } else if (problemCategory === 3) {
      targetCodes.push('CRAFTSMAN_03_LEGAL', 'CRAFTSMAN_07_DESIGN');
    } else {
      targetCodes.push('CRAFTSMAN_05_BATTLE', 'CRAFTSMAN_09_COPYWRITER');
    }

    // 3. 過濾出當前真正可用的技能實體
    const matchedSkills = activeSkills.filter((s) => targetCodes.includes(s.code));
    const allocatedSkillIds: string[] = [];

    // 4. 寫入派工紀錄 (SessionSkillAllocation)
    for (const skill of matchedSkills) {
      const record = await prisma.sessionSkillAllocation.create({
        data: {
          sessionId,
          skillId: skill.id,
          status: 'DISPATCHED',
        },
      });
      allocatedSkillIds.push(record.skillId);
    }

    return {
      sessionId,
      selectedSkillCodes: matchedSkills.map((s) => s.code),
      allocatedSkillIds,
    };
  }
}

核心控管優勢
 * 動態熱插拔（Hot-Swappable）：當某個 Skill 需要維護或產生偏差時，只需在資料庫將 isActive 設為 false，Kernel 在派工時就會自動剔除該技能並改派備援，主程式與 Kernel 算力零停機。
 * 全程可追蹤（Audit Trail）：每次決策「派了哪些小弟、誰回傳了 Evidence、誰被 Kernel 採納」全部有 PostgreSQL 紀錄，責任鏈絕對清晰。

                   ┌─────────────────────────────────────────┐
                    │               L0 OWNER                  │
                    │               ( 唯一老大 )               │
                    └────────────────────┬────────────────────┘
                                         │  唯一下達意圖 & 最高問責
                                         ▼
                    ┌─────────────────────────────────────────┐
                    │              GUBON KERNEL               │
                    │         L1 最高系統統帥 / 裁決者         │
                    └────────────────────┬────────────────────┘
                                         │  動態調度與管理
                                         ▼
                    ┌─────────────────────────────────────────┐
                    │           L2 – L4 十二職人與技能         │
                    │             ( 專業幕僚與執行工具 )       │
                    └─────────────────────────────────────────┘

[ 外部使用者 / 駭客輸入 ]
          │
          ▼
┌──────────────────────────────────────────────────────────┐
│ 1. Cloudflare + Express API (硬性 Validation / 脫敏)     │
└─────────────────────────┬────────────────────────────────┘
                          │
                          ▼
┌──────────────────────────────────────────────────────────┐
│ 2. AI / 12 職人 Skills (純沙盒環境 / 零 DB 寫入權)         │
│    • 僅能產出結構化 Evidence (JSON)                       │
│    • 就算被 Prompt Injection，也只是吐出無效 JSON            │
└─────────────────────────┬────────────────────────────────┘
                          │
                          ▼
┌──────────────────────────────────────────────────────────┐
│ 3. GUBON Kernel (純 TypeScript 確定性邏輯裁決)           │
│    • 對 AI 傳回的資料進行 100% 格式與風控審查             │
│    • 只有 Kernel 程式碼能改寫資料庫狀態                   │
└─────────────────────────┬────────────────────────────────┘
                          │
                          ▼
┌──────────────────────────────────────────────────────────┐
│ 4. L0 Owner 安全閘口 (實體變更必須 Human-in-the-Loop)    │
│    • 超乎報告外的事情，系統硬性鎖死，等待您同意才開鎖    │
└──────────────────────────────────────────────────────────┘

┌───────────────────────────────────────────────────────────┐
│                    AI 無所不能的超強算力                   │
│                       ( 內練於沙盒 )                       │
│  • 12 職人多維分析  • 交叉比對  • 語意編譯  • 證據打包       │
└─────────────────────────────┬─────────────────────────────┘
                              │
                              ▼
┌───────────────────────────────────────────────────────────┐
│                   GUBON Kernel 最高裁決                    │
│                  ( 確定性邏輯 / 嚴格審查 )                 │
└─────────────────────────────┬─────────────────────────────┘
                              │
                              ▼
┌───────────────────────────────────────────────────────────┐
│                  L0 Owner (您) 最高閘口                    │
│             ( 唯一擁有外放/實體執行的開關權 )               │
└───────────────────────────────────────────────────────────┘
