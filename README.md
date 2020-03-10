{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# JSON examples and exercise\n",
    "****\n",
    "+ get familiar with packages for dealing with JSON\n",
    "+ study examples with JSON strings and files \n",
    "+ work on exercise to be completed and submitted \n",
    "****\n",
    "+ reference: http://pandas.pydata.org/pandas-docs/stable/io.html#io-json-reader\n",
    "+ data source: http://jsonstudio.com/resources/\n",
    "****"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": [
    "import pandas as pd\n",
    "import numpy as np #used later for np.nan"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## imports for Python, Pandas"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": [
    "import json\n",
    "from pandas.io.json import json_normalize"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## JSON example, with string\n",
    "\n",
    "+ demonstrates creation of normalized dataframes (tables) from nested json string\n",
    "+ source: http://pandas.pydata.org/pandas-docs/stable/io.html#normalization"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": [
    "# define json string\n",
    "data = [{'state': 'Florida', \n",
    "         'shortname': 'FL',\n",
    "         'info': {'governor': 'Rick Scott'},\n",
    "         'counties': [{'name': 'Dade', 'population': 12345},\n",
    "                      {'name': 'Broward', 'population': 40000},\n",
    "                      {'name': 'Palm Beach', 'population': 60000}]},\n",
    "        {'state': 'Ohio',\n",
    "         'shortname': 'OH',\n",
    "         'info': {'governor': 'John Kasich'},\n",
    "         'counties': [{'name': 'Summit', 'population': 1234},\n",
    "                      {'name': 'Cuyahoga', 'population': 1337}]}]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>name</th>\n",
       "      <th>population</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Dade</td>\n",
       "      <td>12345</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Broward</td>\n",
       "      <td>40000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Palm Beach</td>\n",
       "      <td>60000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Summit</td>\n",
       "      <td>1234</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Cuyahoga</td>\n",
       "      <td>1337</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "         name  population\n",
       "0        Dade       12345\n",
       "1     Broward       40000\n",
       "2  Palm Beach       60000\n",
       "3      Summit        1234\n",
       "4    Cuyahoga        1337"
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# use normalization to create tables from nested element\n",
    "json_normalize(data, 'counties')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>name</th>\n",
       "      <th>population</th>\n",
       "      <th>info.governor</th>\n",
       "      <th>state</th>\n",
       "      <th>shortname</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Dade</td>\n",
       "      <td>12345</td>\n",
       "      <td>Rick Scott</td>\n",
       "      <td>Florida</td>\n",
       "      <td>FL</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Broward</td>\n",
       "      <td>40000</td>\n",
       "      <td>Rick Scott</td>\n",
       "      <td>Florida</td>\n",
       "      <td>FL</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Palm Beach</td>\n",
       "      <td>60000</td>\n",
       "      <td>Rick Scott</td>\n",
       "      <td>Florida</td>\n",
       "      <td>FL</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Summit</td>\n",
       "      <td>1234</td>\n",
       "      <td>John Kasich</td>\n",
       "      <td>Ohio</td>\n",
       "      <td>OH</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Cuyahoga</td>\n",
       "      <td>1337</td>\n",
       "      <td>John Kasich</td>\n",
       "      <td>Ohio</td>\n",
       "      <td>OH</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "         name  population info.governor    state shortname\n",
       "0        Dade       12345    Rick Scott  Florida        FL\n",
       "1     Broward       40000    Rick Scott  Florida        FL\n",
       "2  Palm Beach       60000    Rick Scott  Florida        FL\n",
       "3      Summit        1234   John Kasich     Ohio        OH\n",
       "4    Cuyahoga        1337   John Kasich     Ohio        OH"
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# further populate tables created from nested element\n",
    "json_normalize(data, 'counties', ['state', 'shortname', ['info', 'governor']])"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "****\n",
    "## JSON example, with file\n",
    "\n",
    "+ demonstrates reading in a json file as a string and as a table\n",
    "+ uses small sample file containing data about projects funded by the World Bank \n",
    "+ data source: http://jsonstudio.com/resources/"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[{u'_id': {u'$oid': u'52b213b38594d8a2be17c780'},\n",
       "  u'approvalfy': 1999,\n",
       "  u'board_approval_month': u'November',\n",
       "  u'boardapprovaldate': u'2013-11-12T00:00:00Z',\n",
       "  u'borrower': u'FEDERAL DEMOCRATIC REPUBLIC OF ETHIOPIA',\n",
       "  u'closingdate': u'2018-07-07T00:00:00Z',\n",
       "  u'country_namecode': u'Federal Democratic Republic of Ethiopia!$!ET',\n",
       "  u'countrycode': u'ET',\n",
       "  u'countryname': u'Federal Democratic Republic of Ethiopia',\n",
       "  u'countryshortname': u'Ethiopia',\n",
       "  u'docty': u'Project Information Document,Indigenous Peoples Plan,Project Information Document',\n",
       "  u'envassesmentcategorycode': u'C',\n",
       "  u'grantamt': 0,\n",
       "  u'ibrdcommamt': 0,\n",
       "  u'id': u'P129828',\n",
       "  u'idacommamt': 130000000,\n",
       "  u'impagency': u'MINISTRY OF EDUCATION',\n",
       "  u'lendinginstr': u'Investment Project Financing',\n",
       "  u'lendinginstrtype': u'IN',\n",
       "  u'lendprojectcost': 550000000,\n",
       "  u'majorsector_percent': [{u'Name': u'Education', u'Percent': 46},\n",
       "   {u'Name': u'Education', u'Percent': 26},\n",
       "   {u'Name': u'Public Administration, Law, and Justice', u'Percent': 16},\n",
       "   {u'Name': u'Education', u'Percent': 12}],\n",
       "  u'mjsector_namecode': [{u'code': u'EX', u'name': u'Education'},\n",
       "   {u'code': u'EX', u'name': u'Education'},\n",
       "   {u'code': u'BX', u'name': u'Public Administration, Law, and Justice'},\n",
       "   {u'code': u'EX', u'name': u'Education'}],\n",
       "  u'mjtheme': [u'Human development'],\n",
       "  u'mjtheme_namecode': [{u'code': u'8', u'name': u'Human development'},\n",
       "   {u'code': u'11', u'name': u''}],\n",
       "  u'mjthemecode': u'8,11',\n",
       "  u'prodline': u'PE',\n",
       "  u'prodlinetext': u'IBRD/IDA',\n",
       "  u'productlinetype': u'L',\n",
       "  u'project_abstract': {u'cdata': u'The development objective of the Second Phase of General Education Quality Improvement Project for Ethiopia is to improve learning conditions in primary and secondary schools and strengthen institutions at different levels of educational administration. The project has six components. The first component is curriculum, textbooks, assessment, examinations, and inspection. This component will support improvement of learning conditions in grades KG-12 by providing increased access to teaching and learning materials and through improvements to the curriculum by assessing the strengths and weaknesses of the current curriculum. This component has following four sub-components: (i) curriculum reform and implementation; (ii) teaching and learning materials; (iii) assessment and examinations; and (iv) inspection. The second component is teacher development program (TDP). This component will support improvements in learning conditions in both primary and secondary schools by advancing the quality of teaching in general education through: (a) enhancing the training of pre-service teachers in teacher education institutions; and (b) improving the quality of in-service teacher training. This component has following three sub-components: (i) pre-service teacher training; (ii) in-service teacher training; and (iii) licensing and relicensing of teachers and school leaders. The third component is school improvement plan. This component will support the strengthening of school planning in order to improve learning outcomes, and to partly fund the school improvement plans through school grants. It has following two sub-components: (i) school improvement plan; and (ii) school grants. The fourth component is management and capacity building, including education management information systems (EMIS). This component will support management and capacity building aspect of the project. This component has following three sub-components: (i) capacity building for education planning and management; (ii) capacity building for school planning and management; and (iii) EMIS. The fifth component is improving the quality of learning and teaching in secondary schools and universities through the use of information and communications technology (ICT). It has following five sub-components: (i) national policy and institution for ICT in general education; (ii) national ICT infrastructure improvement plan for general education; (iii) develop an integrated monitoring, evaluation, and learning system specifically for the ICT component; (iv) teacher professional development in the use of ICT; and (v) provision of limited number of e-Braille display readers with the possibility to scale up to all secondary education schools based on the successful implementation and usage of the readers. The sixth component is program coordination, monitoring and evaluation, and communication. It will support institutional strengthening by developing capacities in all aspects of program coordination, monitoring and evaluation; a new sub-component on communications will support information sharing for better management and accountability. It has following three sub-components: (i) program coordination; (ii) monitoring and evaluation (M and E); and (iii) communication.'},\n",
       "  u'project_name': u'Ethiopia General Education Quality Improvement Project II',\n",
       "  u'projectdocs': [{u'DocDate': u'28-AUG-2013',\n",
       "    u'DocType': u'PID',\n",
       "    u'DocTypeDesc': u'Project Information Document (PID),  Vol.',\n",
       "    u'DocURL': u'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=090224b081e545fb_1_0',\n",
       "    u'EntityID': u'090224b081e545fb_1_0'},\n",
       "   {u'DocDate': u'01-JUL-2013',\n",
       "    u'DocType': u'IP',\n",
       "    u'DocTypeDesc': u'Indigenous Peoples Plan (IP),  Vol.1 of 1',\n",
       "    u'DocURL': u'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000442464_20130920111729',\n",
       "    u'EntityID': u'000442464_20130920111729'},\n",
       "   {u'DocDate': u'22-NOV-2012',\n",
       "    u'DocType': u'PID',\n",
       "    u'DocTypeDesc': u'Project Information Document (PID),  Vol.',\n",
       "    u'DocURL': u'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=090224b0817b19e2_1_0',\n",
       "    u'EntityID': u'090224b0817b19e2_1_0'}],\n",
       "  u'projectfinancialtype': u'IDA',\n",
       "  u'projectstatusdisplay': u'Active',\n",
       "  u'regionname': u'Africa',\n",
       "  u'sector': [{u'Name': u'Primary education'},\n",
       "   {u'Name': u'Secondary education'},\n",
       "   {u'Name': u'Public administration- Other social services'},\n",
       "   {u'Name': u'Tertiary education'}],\n",
       "  u'sector1': {u'Name': u'Primary education', u'Percent': 46},\n",
       "  u'sector2': {u'Name': u'Secondary education', u'Percent': 26},\n",
       "  u'sector3': {u'Name': u'Public administration- Other social services',\n",
       "   u'Percent': 16},\n",
       "  u'sector4': {u'Name': u'Tertiary education', u'Percent': 12},\n",
       "  u'sector_namecode': [{u'code': u'EP', u'name': u'Primary education'},\n",
       "   {u'code': u'ES', u'name': u'Secondary education'},\n",
       "   {u'code': u'BS', u'name': u'Public administration- Other social services'},\n",
       "   {u'code': u'ET', u'name': u'Tertiary education'}],\n",
       "  u'sectorcode': u'ET,BS,ES,EP',\n",
       "  u'source': u'IBRD',\n",
       "  u'status': u'Active',\n",
       "  u'supplementprojectflg': u'N',\n",
       "  u'theme1': {u'Name': u'Education for all', u'Percent': 100},\n",
       "  u'theme_namecode': [{u'code': u'65', u'name': u'Education for all'}],\n",
       "  u'themecode': u'65',\n",
       "  u'totalamt': 130000000,\n",
       "  u'totalcommamt': 130000000,\n",
       "  u'url': u'http://www.worldbank.org/projects/P129828/ethiopia-general-education-quality-improvement-project-ii?lang=en'},\n",
       " {u'_id': {u'$oid': u'52b213b38594d8a2be17c781'},\n",
       "  u'approvalfy': 2015,\n",
       "  u'board_approval_month': u'November',\n",
       "  u'boardapprovaldate': u'2013-11-04T00:00:00Z',\n",
       "  u'borrower': u'GOVERNMENT OF TUNISIA',\n",
       "  u'country_namecode': u'Republic of Tunisia!$!TN',\n",
       "  u'countrycode': u'TN',\n",
       "  u'countryname': u'Republic of Tunisia',\n",
       "  u'countryshortname': u'Tunisia',\n",
       "  u'docty': u'Project Information Document,Integrated Safeguards Data Sheet,Integrated Safeguards Data Sheet,Project Information Document,Integrated Safeguards Data Sheet,Project Information Document',\n",
       "  u'envassesmentcategorycode': u'C',\n",
       "  u'grantamt': 4700000,\n",
       "  u'ibrdcommamt': 0,\n",
       "  u'id': u'P144674',\n",
       "  u'idacommamt': 0,\n",
       "  u'impagency': u'MINISTRY OF FINANCE',\n",
       "  u'lendinginstr': u'Specific Investment Loan',\n",
       "  u'lendinginstrtype': u'IN',\n",
       "  u'lendprojectcost': 5700000,\n",
       "  u'majorsector_percent': [{u'Name': u'Public Administration, Law, and Justice',\n",
       "    u'Percent': 70},\n",
       "   {u'Name': u'Public Administration, Law, and Justice', u'Percent': 30}],\n",
       "  u'mjsector_namecode': [{u'code': u'BX',\n",
       "    u'name': u'Public Administration, Law, and Justice'},\n",
       "   {u'code': u'BX', u'name': u'Public Administration, Law, and Justice'}],\n",
       "  u'mjtheme': [u'Economic management',\n",
       "   u'Social protection and risk management'],\n",
       "  u'mjtheme_namecode': [{u'code': u'1', u'name': u'Economic management'},\n",
       "   {u'code': u'6', u'name': u'Social protection and risk management'}],\n",
       "  u'mjthemecode': u'1,6',\n",
       "  u'prodline': u'RE',\n",
       "  u'prodlinetext': u'Recipient Executed Activities',\n",
       "  u'productlinetype': u'L',\n",
       "  u'project_name': u'TN: DTF Social Protection Reforms Support',\n",
       "  u'projectdocs': [{u'DocDate': u'29-MAR-2013',\n",
       "    u'DocType': u'PID',\n",
       "    u'DocTypeDesc': u'Project Information Document (PID),  Vol.1 of 1',\n",
       "    u'DocURL': u'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000333037_20131024115616',\n",
       "    u'EntityID': u'000333037_20131024115616'},\n",
       "   {u'DocDate': u'29-MAR-2013',\n",
       "    u'DocType': u'ISDS',\n",
       "    u'DocTypeDesc': u'Integrated Safeguards Data Sheet (ISDS),  Vol.1 of 1',\n",
       "    u'DocURL': u'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000356161_20131024151611',\n",
       "    u'EntityID': u'000356161_20131024151611'},\n",
       "   {u'DocDate': u'29-MAR-2013',\n",
       "    u'DocType': u'ISDS',\n",
       "    u'DocTypeDesc': u'Integrated Safeguards Data Sheet (ISDS),  Vol.1 of 1',\n",
       "    u'DocURL': u'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000442464_20131031112136',\n",
       "    u'EntityID': u'000442464_20131031112136'},\n",
       "   {u'DocDate': u'29-MAR-2013',\n",
       "    u'DocType': u'PID',\n",
       "    u'DocTypeDesc': u'Project Information Document (PID),  Vol.1 of 1',\n",
       "    u'DocURL': u'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000333037_20131031105716',\n",
       "    u'EntityID': u'000333037_20131031105716'},\n",
       "   {u'DocDate': u'16-JAN-2013',\n",
       "    u'DocType': u'ISDS',\n",
       "    u'DocTypeDesc': u'Integrated Safeguards Data Sheet (ISDS),  Vol.1 of 1',\n",
       "    u'DocURL': u'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000356161_20130305113209',\n",
       "    u'EntityID': u'000356161_20130305113209'},\n",
       "   {u'DocDate': u'16-JAN-2013',\n",
       "    u'DocType': u'PID',\n",
       "    u'DocTypeDesc': u'Project Information Document (PID),  Vol.1 of 1',\n",
       "    u'DocURL': u'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000356161_20130305113716',\n",
       "    u'EntityID': u'000356161_20130305113716'}],\n",
       "  u'projectfinancialtype': u'OTHER',\n",
       "  u'projectstatusdisplay': u'Active',\n",
       "  u'regionname': u'Middle East and North Africa',\n",
       "  u'sector': [{u'Name': u'Public administration- Other social services'},\n",
       "   {u'Name': u'General public administration sector'}],\n",
       "  u'sector1': {u'Name': u'Public administration- Other social services',\n",
       "   u'Percent': 70},\n",
       "  u'sector2': {u'Name': u'General public administration sector',\n",
       "   u'Percent': 30},\n",
       "  u'sector_namecode': [{u'code': u'BS',\n",
       "    u'name': u'Public administration- Other social services'},\n",
       "   {u'code': u'BZ', u'name': u'General public administration sector'}],\n",
       "  u'sectorcode': u'BZ,BS',\n",
       "  u'source': u'IBRD',\n",
       "  u'status': u'Active',\n",
       "  u'supplementprojectflg': u'N',\n",
       "  u'theme1': {u'Name': u'Other economic management', u'Percent': 30},\n",
       "  u'theme_namecode': [{u'code': u'24', u'name': u'Other economic management'},\n",
       "   {u'code': u'54', u'name': u'Social safety nets'}],\n",
       "  u'themecode': u'54,24',\n",
       "  u'totalamt': 0,\n",
       "  u'totalcommamt': 4700000,\n",
       "  u'url': u'http://www.worldbank.org/projects/P144674?lang=en'}]"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# load json as string\n",
    "json.load((open('data/world_bank_projects_less.json')))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>_id</th>\n",
       "      <th>approvalfy</th>\n",
       "      <th>board_approval_month</th>\n",
       "      <th>boardapprovaldate</th>\n",
       "      <th>borrower</th>\n",
       "      <th>closingdate</th>\n",
       "      <th>country_namecode</th>\n",
       "      <th>countrycode</th>\n",
       "      <th>countryname</th>\n",
       "      <th>countryshortname</th>\n",
       "      <th>...</th>\n",
       "      <th>sectorcode</th>\n",
       "      <th>source</th>\n",
       "      <th>status</th>\n",
       "      <th>supplementprojectflg</th>\n",
       "      <th>theme1</th>\n",
       "      <th>theme_namecode</th>\n",
       "      <th>themecode</th>\n",
       "      <th>totalamt</th>\n",
       "      <th>totalcommamt</th>\n",
       "      <th>url</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>{u'$oid': u'52b213b38594d8a2be17c780'}</td>\n",
       "      <td>1999</td>\n",
       "      <td>November</td>\n",
       "      <td>2013-11-12T00:00:00Z</td>\n",
       "      <td>FEDERAL DEMOCRATIC REPUBLIC OF ETHIOPIA</td>\n",
       "      <td>2018-07-07T00:00:00Z</td>\n",
       "      <td>Federal Democratic Republic of Ethiopia!$!ET</td>\n",
       "      <td>ET</td>\n",
       "      <td>Federal Democratic Republic of Ethiopia</td>\n",
       "      <td>Ethiopia</td>\n",
       "      <td>...</td>\n",
       "      <td>ET,BS,ES,EP</td>\n",
       "      <td>IBRD</td>\n",
       "      <td>Active</td>\n",
       "      <td>N</td>\n",
       "      <td>{u'Percent': 100, u'Name': u'Education for all'}</td>\n",
       "      <td>[{u'code': u'65', u'name': u'Education for all'}]</td>\n",
       "      <td>65</td>\n",
       "      <td>130000000</td>\n",
       "      <td>130000000</td>\n",
       "      <td>http://www.worldbank.org/projects/P129828/ethi...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>{u'$oid': u'52b213b38594d8a2be17c781'}</td>\n",
       "      <td>2015</td>\n",
       "      <td>November</td>\n",
       "      <td>2013-11-04T00:00:00Z</td>\n",
       "      <td>GOVERNMENT OF TUNISIA</td>\n",
       "      <td>NaN</td>\n",
       "      <td>Republic of Tunisia!$!TN</td>\n",
       "      <td>TN</td>\n",
       "      <td>Republic of Tunisia</td>\n",
       "      <td>Tunisia</td>\n",
       "      <td>...</td>\n",
       "      <td>BZ,BS</td>\n",
       "      <td>IBRD</td>\n",
       "      <td>Active</td>\n",
       "      <td>N</td>\n",
       "      <td>{u'Percent': 30, u'Name': u'Other economic man...</td>\n",
       "      <td>[{u'code': u'24', u'name': u'Other economic ma...</td>\n",
       "      <td>54,24</td>\n",
       "      <td>0</td>\n",
       "      <td>4700000</td>\n",
       "      <td>http://www.worldbank.org/projects/P144674?lang=en</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>2 rows × 50 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                                      _id  approvalfy board_approval_month  \\\n",
       "0  {u'$oid': u'52b213b38594d8a2be17c780'}        1999             November   \n",
       "1  {u'$oid': u'52b213b38594d8a2be17c781'}        2015             November   \n",
       "\n",
       "      boardapprovaldate                                 borrower  \\\n",
       "0  2013-11-12T00:00:00Z  FEDERAL DEMOCRATIC REPUBLIC OF ETHIOPIA   \n",
       "1  2013-11-04T00:00:00Z                    GOVERNMENT OF TUNISIA   \n",
       "\n",
       "            closingdate                              country_namecode  \\\n",
       "0  2018-07-07T00:00:00Z  Federal Democratic Republic of Ethiopia!$!ET   \n",
       "1                   NaN                      Republic of Tunisia!$!TN   \n",
       "\n",
       "  countrycode                              countryname countryshortname  \\\n",
       "0          ET  Federal Democratic Republic of Ethiopia         Ethiopia   \n",
       "1          TN                      Republic of Tunisia          Tunisia   \n",
       "\n",
       "                         ...                           sectorcode source  \\\n",
       "0                        ...                          ET,BS,ES,EP   IBRD   \n",
       "1                        ...                                BZ,BS   IBRD   \n",
       "\n",
       "   status  supplementprojectflg  \\\n",
       "0  Active                     N   \n",
       "1  Active                     N   \n",
       "\n",
       "                                              theme1  \\\n",
       "0   {u'Percent': 100, u'Name': u'Education for all'}   \n",
       "1  {u'Percent': 30, u'Name': u'Other economic man...   \n",
       "\n",
       "                                      theme_namecode themecode   totalamt  \\\n",
       "0  [{u'code': u'65', u'name': u'Education for all'}]        65  130000000   \n",
       "1  [{u'code': u'24', u'name': u'Other economic ma...     54,24          0   \n",
       "\n",
       "  totalcommamt                                                url  \n",
       "0    130000000  http://www.worldbank.org/projects/P129828/ethi...  \n",
       "1      4700000  http://www.worldbank.org/projects/P144674?lang=en  \n",
       "\n",
       "[2 rows x 50 columns]"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# load as Pandas dataframe\n",
    "sample_json_df = pd.read_json('data/world_bank_projects_less.json')\n",
    "sample_json_df"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "****\n",
    "## JSON exercise\n",
    "\n",
    "Using data in file 'data/world_bank_projects.json' and the techniques demonstrated above,\n",
    "1. Find the 10 countries with most projects\n",
    "2. Find the top 10 major project themes (using column 'mjtheme_namecode')\n",
    "3. In 2. above you will notice that some entries have only the code and the name is missing. Create a dataframe with the missing names filled in."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "collapsed": true
   },
   "source": [
    "# # Start of Code by J Mayer"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Problem #1: Find the 10 countries with most projects"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>_id</th>\n",
       "      <th>approvalfy</th>\n",
       "      <th>board_approval_month</th>\n",
       "      <th>boardapprovaldate</th>\n",
       "      <th>borrower</th>\n",
       "      <th>closingdate</th>\n",
       "      <th>country_namecode</th>\n",
       "      <th>countrycode</th>\n",
       "      <th>countryname</th>\n",
       "      <th>countryshortname</th>\n",
       "      <th>...</th>\n",
       "      <th>sectorcode</th>\n",
       "      <th>source</th>\n",
       "      <th>status</th>\n",
       "      <th>supplementprojectflg</th>\n",
       "      <th>theme1</th>\n",
       "      <th>theme_namecode</th>\n",
       "      <th>themecode</th>\n",
       "      <th>totalamt</th>\n",
       "      <th>totalcommamt</th>\n",
       "      <th>url</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>{u'$oid': u'52b213b38594d8a2be17c780'}</td>\n",
       "      <td>1999</td>\n",
       "      <td>November</td>\n",
       "      <td>2013-11-12T00:00:00Z</td>\n",
       "      <td>FEDERAL DEMOCRATIC REPUBLIC OF ETHIOPIA</td>\n",
       "      <td>2018-07-07T00:00:00Z</td>\n",
       "      <td>Federal Democratic Republic of Ethiopia!$!ET</td>\n",
       "      <td>ET</td>\n",
       "      <td>Federal Democratic Republic of Ethiopia</td>\n",
       "      <td>Ethiopia</td>\n",
       "      <td>...</td>\n",
       "      <td>ET,BS,ES,EP</td>\n",
       "      <td>IBRD</td>\n",
       "      <td>Active</td>\n",
       "      <td>N</td>\n",
       "      <td>{u'Percent': 100, u'Name': u'Education for all'}</td>\n",
       "      <td>[{u'code': u'65', u'name': u'Education for all'}]</td>\n",
       "      <td>65</td>\n",
       "      <td>130000000</td>\n",
       "      <td>130000000</td>\n",
       "      <td>http://www.worldbank.org/projects/P129828/ethi...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>{u'$oid': u'52b213b38594d8a2be17c781'}</td>\n",
       "      <td>2015</td>\n",
       "      <td>November</td>\n",
       "      <td>2013-11-04T00:00:00Z</td>\n",
       "      <td>GOVERNMENT OF TUNISIA</td>\n",
       "      <td>NaN</td>\n",
       "      <td>Republic of Tunisia!$!TN</td>\n",
       "      <td>TN</td>\n",
       "      <td>Republic of Tunisia</td>\n",
       "      <td>Tunisia</td>\n",
       "      <td>...</td>\n",
       "      <td>BZ,BS</td>\n",
       "      <td>IBRD</td>\n",
       "      <td>Active</td>\n",
       "      <td>N</td>\n",
       "      <td>{u'Percent': 30, u'Name': u'Other economic man...</td>\n",
       "      <td>[{u'code': u'24', u'name': u'Other economic ma...</td>\n",
       "      <td>54,24</td>\n",
       "      <td>0</td>\n",
       "      <td>4700000</td>\n",
       "      <td>http://www.worldbank.org/projects/P144674?lang=en</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>{u'$oid': u'52b213b38594d8a2be17c782'}</td>\n",
       "      <td>2014</td>\n",
       "      <td>November</td>\n",
       "      <td>2013-11-01T00:00:00Z</td>\n",
       "      <td>MINISTRY OF FINANCE AND ECONOMIC DEVEL</td>\n",
       "      <td>NaN</td>\n",
       "      <td>Tuvalu!$!TV</td>\n",
       "      <td>TV</td>\n",
       "      <td>Tuvalu</td>\n",
       "      <td>Tuvalu</td>\n",
       "      <td>...</td>\n",
       "      <td>TI</td>\n",
       "      <td>IBRD</td>\n",
       "      <td>Active</td>\n",
       "      <td>Y</td>\n",
       "      <td>{u'Percent': 46, u'Name': u'Regional integrati...</td>\n",
       "      <td>[{u'code': u'47', u'name': u'Regional integrat...</td>\n",
       "      <td>52,81,25,47</td>\n",
       "      <td>6060000</td>\n",
       "      <td>6060000</td>\n",
       "      <td>http://www.worldbank.org/projects/P145310?lang=en</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>3 rows × 50 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                                      _id  approvalfy board_approval_month  \\\n",
       "0  {u'$oid': u'52b213b38594d8a2be17c780'}        1999             November   \n",
       "1  {u'$oid': u'52b213b38594d8a2be17c781'}        2015             November   \n",
       "2  {u'$oid': u'52b213b38594d8a2be17c782'}        2014             November   \n",
       "\n",
       "      boardapprovaldate                                 borrower  \\\n",
       "0  2013-11-12T00:00:00Z  FEDERAL DEMOCRATIC REPUBLIC OF ETHIOPIA   \n",
       "1  2013-11-04T00:00:00Z                    GOVERNMENT OF TUNISIA   \n",
       "2  2013-11-01T00:00:00Z   MINISTRY OF FINANCE AND ECONOMIC DEVEL   \n",
       "\n",
       "            closingdate                              country_namecode  \\\n",
       "0  2018-07-07T00:00:00Z  Federal Democratic Republic of Ethiopia!$!ET   \n",
       "1                   NaN                      Republic of Tunisia!$!TN   \n",
       "2                   NaN                                   Tuvalu!$!TV   \n",
       "\n",
       "  countrycode                              countryname countryshortname  \\\n",
       "0          ET  Federal Democratic Republic of Ethiopia         Ethiopia   \n",
       "1          TN                      Republic of Tunisia          Tunisia   \n",
       "2          TV                                   Tuvalu           Tuvalu   \n",
       "\n",
       "                         ...                           sectorcode source  \\\n",
       "0                        ...                          ET,BS,ES,EP   IBRD   \n",
       "1                        ...                                BZ,BS   IBRD   \n",
       "2                        ...                                   TI   IBRD   \n",
       "\n",
       "   status  supplementprojectflg  \\\n",
       "0  Active                     N   \n",
       "1  Active                     N   \n",
       "2  Active                     Y   \n",
       "\n",
       "                                              theme1  \\\n",
       "0   {u'Percent': 100, u'Name': u'Education for all'}   \n",
       "1  {u'Percent': 30, u'Name': u'Other economic man...   \n",
       "2  {u'Percent': 46, u'Name': u'Regional integrati...   \n",
       "\n",
       "                                      theme_namecode    themecode   totalamt  \\\n",
       "0  [{u'code': u'65', u'name': u'Education for all'}]           65  130000000   \n",
       "1  [{u'code': u'24', u'name': u'Other economic ma...        54,24          0   \n",
       "2  [{u'code': u'47', u'name': u'Regional integrat...  52,81,25,47    6060000   \n",
       "\n",
       "  totalcommamt                                                url  \n",
       "0    130000000  http://www.worldbank.org/projects/P129828/ethi...  \n",
       "1      4700000  http://www.worldbank.org/projects/P144674?lang=en  \n",
       "2      6060000  http://www.worldbank.org/projects/P145310?lang=en  \n",
       "\n",
       "[3 rows x 50 columns]"
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#load data\n",
    "df = pd.read_json('data/world_bank_projects.json')\n",
    "df.head(3) #always call head for structure of table and name of cols"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "Int64Index: 500 entries, 0 to 499\n",
      "Data columns (total 50 columns):\n",
      "_id                         500 non-null object\n",
      "approvalfy                  500 non-null int64\n",
      "board_approval_month        500 non-null object\n",
      "boardapprovaldate           500 non-null object\n",
      "borrower                    485 non-null object\n",
      "closingdate                 370 non-null object\n",
      "country_namecode            500 non-null object\n",
      "countrycode                 500 non-null object\n",
      "countryname                 500 non-null object\n",
      "countryshortname            500 non-null object\n",
      "docty                       446 non-null object\n",
      "envassesmentcategorycode    430 non-null object\n",
      "grantamt                    500 non-null int64\n",
      "ibrdcommamt                 500 non-null int64\n",
      "id                          500 non-null object\n",
      "idacommamt                  500 non-null int64\n",
      "impagency                   472 non-null object\n",
      "lendinginstr                495 non-null object\n",
      "lendinginstrtype            495 non-null object\n",
      "lendprojectcost             500 non-null int64\n",
      "majorsector_percent         500 non-null object\n",
      "mjsector_namecode           500 non-null object\n",
      "mjtheme                     491 non-null object\n",
      "mjtheme_namecode            500 non-null object\n",
      "mjthemecode                 500 non-null object\n",
      "prodline                    500 non-null object\n",
      "prodlinetext                500 non-null object\n",
      "productlinetype             500 non-null object\n",
      "project_abstract            362 non-null object\n",
      "project_name                500 non-null object\n",
      "projectdocs                 446 non-null object\n",
      "projectfinancialtype        500 non-null object\n",
      "projectstatusdisplay        500 non-null object\n",
      "regionname                  500 non-null object\n",
      "sector                      500 non-null object\n",
      "sector1                     500 non-null object\n",
      "sector2                     380 non-null object\n",
      "sector3                     265 non-null object\n",
      "sector4                     174 non-null object\n",
      "sector_namecode             500 non-null object\n",
      "sectorcode                  500 non-null object\n",
      "source                      500 non-null object\n",
      "status                      500 non-null object\n",
      "supplementprojectflg        498 non-null object\n",
      "theme1                      500 non-null object\n",
      "theme_namecode              491 non-null object\n",
      "themecode                   491 non-null object\n",
      "totalamt                    500 non-null int64\n",
      "totalcommamt                500 non-null int64\n",
      "url                         500 non-null object\n",
      "dtypes: int64(7), object(43)\n",
      "memory usage: 199.2+ KB\n"
     ]
    }
   ],
   "source": [
    "df.info() #checking contents of df"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Appears that we have 500 rows of data, although some columns have missing (null) data. Will explore this later if necessary. For now, proceed with analysis on 'countryname' col since it contains 500 non-null values. "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Problem #1: Find the 10 countries with most projects"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "countryname\n",
       "People's Republic of China         19\n",
       "Republic of Indonesia              19\n",
       "Socialist Republic of Vietnam      17\n",
       "Republic of India                  16\n",
       "Republic of Yemen                  13\n",
       "Nepal                              12\n",
       "People's Republic of Bangladesh    12\n",
       "Kingdom of Morocco                 12\n",
       "Africa                             11\n",
       "Republic of Mozambique             11\n",
       "dtype: int64"
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#use some of the nifty tricks I learned in the pandas tutorial\n",
    "df.groupby('countryname').size().sort_values(ascending=False).head(10)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Problem #2: Find the top 10 major project themes (using column 'mjtheme_namecode')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {
    "collapsed": false
   },
   "outputs": [],
   "source": [
    "#In order to complete this we need to leverage the json_normalize function which requires loading json as a string\n",
    "#load json as string\n",
    "new_data = json.load((open('data/world_bank_projects.json')))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>code</th>\n",
       "      <th>name</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>8</td>\n",
       "      <td>Human development</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>11</td>\n",
       "      <td></td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>1</td>\n",
       "      <td>Economic management</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>6</td>\n",
       "      <td>Social protection and risk management</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>5</td>\n",
       "      <td>Trade and integration</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "  code                                   name\n",
       "0    8                      Human development\n",
       "1   11                                       \n",
       "2    1                    Economic management\n",
       "3    6  Social protection and risk management\n",
       "4    5                  Trade and integration"
      ]
     },
     "execution_count": 13,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#use json_normalize function to access nested information\n",
    "df3 = json_normalize(new_data, 'mjtheme_namecode')\n",
    "df3.head() #appears that we have missing information in the 'name' col "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "name\n",
       "Environment and natural resources management    223\n",
       "Rural development                               202\n",
       "Human development                               197\n",
       "Public sector governance                        184\n",
       "Social protection and risk management           158\n",
       "Financial and private sector development        130\n",
       "                                                122\n",
       "Social dev/gender/inclusion                     119\n",
       "Trade and integration                            72\n",
       "Urban development                                47\n",
       "dtype: int64"
      ]
     },
     "execution_count": 16,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#here is the tentative answer to #2, BUT we notice that we have names missing. \n",
    "#We will re-run this after we solve problem #3. \n",
    "df3.groupby(['name']).size().sort_values(ascending=False).head(10)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "code\n",
       "11    250\n",
       "10    216\n",
       "8     210\n",
       "2     199\n",
       "6     168\n",
       "4     146\n",
       "7     130\n",
       "5      77\n",
       "9      50\n",
       "1      38\n",
       "dtype: int64"
      ]
     },
     "execution_count": 17,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#here is the answer we should see after we solve problem #3\n",
    "df3.groupby(['code']).size().sort_values(ascending=False).head(10)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "RangeIndex: 1499 entries, 0 to 1498\n",
      "Data columns (total 2 columns):\n",
      "code    1499 non-null object\n",
      "name    1499 non-null object\n",
      "dtypes: object(2)\n",
      "memory usage: 23.5+ KB\n"
     ]
    }
   ],
   "source": [
    "df3.info() #hmmm... all non-null values. Must be because we are importing empty strings"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## It appears that the names of the codes are consistent, but that some of the codes do not have the appropriate associated name. Let's fix this by filling in the appropriate name in the empty string based on associated 'code'."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "metadata": {
    "collapsed": false
   },
   "outputs": [],
   "source": [
    "df5 = df3.sort_values(['code', 'name'], ascending=True) #sorting so that we can use the fillna function to fill later"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "Int64Index: 1499 entries, 212 to 1495\n",
      "Data columns (total 2 columns):\n",
      "code    1499 non-null object\n",
      "name    1499 non-null object\n",
      "dtypes: object(2)\n",
      "memory usage: 35.1+ KB\n"
     ]
    }
   ],
   "source": [
    "#replacing empty strings with NaN so that we can use fillna()\n",
    "df5.replace(to_replace='', value=np.nan, inplace=True)\n",
    "df5['name'].fillna(inplace=True, method='bfill') #due to the way we sorted earlier, we can 'bfill' with known values\n",
    "df5.info() #confirm non-null objects"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "code  name                                        \n",
       "11    Environment and natural resources management    250\n",
       "10    Rural development                               216\n",
       "8     Human development                               210\n",
       "2     Public sector governance                        199\n",
       "6     Social protection and risk management           168\n",
       "4     Financial and private sector development        146\n",
       "7     Social dev/gender/inclusion                     130\n",
       "5     Trade and integration                            77\n",
       "9     Urban development                                50\n",
       "1     Economic management                              38\n",
       "3     Rule of law                                      15\n",
       "dtype: int64"
      ]
     },
     "execution_count": 23,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#this should be the correct answer to #2, let's check again by calling on the original dataframe (df3) next\n",
    "df5.groupby(['code', 'name']).size().sort_values(ascending=False)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 24,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "code\n",
       "11    250\n",
       "10    216\n",
       "8     210\n",
       "2     199\n",
       "6     168\n",
       "4     146\n",
       "7     130\n",
       "5      77\n",
       "9      50\n",
       "1      38\n",
       "3      15\n",
       "dtype: int64"
      ]
     },
     "execution_count": 24,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#confirmed that we have the same answers, yay!\n",
    "df3.groupby(['code']).size().sort_values(ascending=False)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Answer #3: In 2. above you will notice that some entries have only the code and the name is missing. Create a dataframe with the missing names filled in."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>code</th>\n",
       "      <th>name</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>8</td>\n",
       "      <td>Human development</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>11</td>\n",
       "      <td>Environment and natural resources management</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>1</td>\n",
       "      <td>Economic management</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>6</td>\n",
       "      <td>Social protection and risk management</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>5</td>\n",
       "      <td>Trade and integration</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>2</td>\n",
       "      <td>Public sector governance</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>6</th>\n",
       "      <td>11</td>\n",
       "      <td>Environment and natural resources management</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>7</th>\n",
       "      <td>6</td>\n",
       "      <td>Social protection and risk management</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>8</th>\n",
       "      <td>7</td>\n",
       "      <td>Social dev/gender/inclusion</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>9</th>\n",
       "      <td>7</td>\n",
       "      <td>Social dev/gender/inclusion</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "  code                                          name\n",
       "0    8                             Human development\n",
       "1   11  Environment and natural resources management\n",
       "2    1                           Economic management\n",
       "3    6         Social protection and risk management\n",
       "4    5                         Trade and integration\n",
       "5    2                      Public sector governance\n",
       "6   11  Environment and natural resources management\n",
       "7    6         Social protection and risk management\n",
       "8    7                   Social dev/gender/inclusion\n",
       "9    7                   Social dev/gender/inclusion"
      ]
     },
     "execution_count": 25,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#here is the dataframe that we built earlier\n",
    "df5.sort_index().head(10)"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 2",
   "language": "python",
   "name": "python2"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 2
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython2",
   "version": "2.7.11"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 0
}
